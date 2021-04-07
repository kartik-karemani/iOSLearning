- Core Data is a framework used to persist the data for the application. It is used to handle the model layer of the application.
- In Core Data we create a schema(i.e. NSManagedObjectModel. File with extension .xcdatamodeld) which have multiple entities. It describes the properties of the enties and relationship with other Entity(instance of NSEntityDescription). Entity can be thought as a table in a data base.
- Entity class is sublcass of NSManagedObject.

Abstract Entity : Specify an entity as abstract if you are not initializing it directly. Generally a entity from which many other entity inherit is marked as abstract. It indicates that CoreData is not instantiating it directly.
Entity Inhertiance : It is similar to class inheritance where the common properties are for few are kept in parent entity and other other inherit from it.

Entity Properties : Attributes and Relationship.
- Core Data supports one to one or one to many relation ships.

- Core Data stack contains 4 objects : NSManagedObjectModel, NSManagedObjectContext, NSPersistanceStoreCoordinator, NSPeristanceStore.

NSPersistanceStore - NSPersistance store handles the creation of Core Data Stack.
NSManagedObjectModel - It is the schema which has info about the application data. Like list of entities and along the attribute details and relation ship between the entities.This is loaded in memory which is the first step of core data creation then persistance store coordinator is created.
NSPersistanceStoreCoordinator - It creates new instance of entity in the model and retrives the existing entity from the peristance store. An app can have muliple persistance store managed by persistance store coordinator.
NSManagedObjectContext - This is exposed to the rest of the application. It is like a scratch pad. The object fetched from the persitance store is copied here and any changes made to the object will not reflect in persistance store unless the context is saved.

Creating the Managed Object:
- It requires 2 things i.e. : Entity description and managed object context.Example: 
**let employee = NSEntityDescription.insertNewObjectForEntityForName("Employee", inManagedObjectContext: managedObjectContext) as! EmployeeMO**


- Creation of NSManagedObject doesnot guarantee that it will be persisted. We need to explicitly save the managed object context.
**do {
    try managedObjectContext.save()
} catch {
    fatalError("Failure to save context: \(error)")
}**

Their can be a relationship between 2 NSManagedObject.
i.e Source entity and destination entity.

- To fetch the objects stored in the Persistance store we can use NSFetchRequest.
**let moc = …
let employeesFetch = NSFetchRequest(entityName: "Employee")
 
do {
    let fetchedEmployees = try moc.executeFetchRequest(employeesFetch) as! [EmployeeMO]
} catch {
    fatalError("Failed to fetch employees: \(error)")
}**


- In case we want to filter the result based on some condition then we can use predicate.
**let firstName = "Trevor"
fetchRequest.predicate = NSPredicate(format: "firstName == %@", firstName)**

Core Data will automatically create the accessor methods for the properties defined in the entity.

- When NSManagedObjct is created it is initialised with default values. But we can customize the initialization by overriding awakeFromInsert method. This is called only once in the object life cycle. it is called after you invoke : **initWithEntity:insertIntoManagedObjectContext: or insertNewObjectForEntityForName:inManagedObjectContext:**.
For ex:
**override func awakeFromInsert() {
    super.awakeFromInsert()
    creationDate = NSDate()
}**


In iOS if we are using table view based layout to display data fetched from Core Data then we can use NSFetchedResultController.
Initially we need to create an instance of NSFetchResultController. It required NSFetchRequest and managed object context. Then call performFetch, this will fetch the initial info from core data and monitors the changes in managed object context.
We need to confirm to NSFEtchResultControllerDelegate protocol inorder to automatically update tableview if their is any underline changes in the context. 

We can move the core data initialization code into seperate object to keep the AppDelegate clean.

**Managed Objects and references:**
By default managed object and managed object context have weak referece to each other. Exception here is : managed object context have strong reference to object that are changed until they are saved. 
To make context to keep strong reference of the managed objects we can set :  retainsRegisteredObjects as true.

If NSManagedObjects are related to each other then they have strong reference to each other. This may cause memory leak so when these objects are no longer needed the we can invoke : refreshObject:mergeChanges:  method.
Types of relationship:
to-one
to-many
many-many

Relationship Delete Rules : Following rules specifies what should happen to destination objects when source object is deleted.
1. Deny - If their is at least one object at the destination then do not delete the source object.
2. Nullify - It will remove the relationship and do not delete either of the object.
3. Cascade - Deleting the source object will delete all the destination objects as well.
4. No Action - No not delete the destination objects.

Cross store relationshhip is not supported in Core Data.
Fetched properties are weak one way relationship.

A managed object is said to be a fault if their properties are not yet loaded from the store.
If persistance object of the Fault managed object is accessed then core data will fetch the data and initializes the property. This is called as Firing the Faults.

A application can have multiple managed object context. If objects in multiple context represents the same data and changes in them wrt context lead to conflict while saving the managed object context.

For ex if application have multiple managed object context and single persistant store coordinator and object is deleted in moc1 then it needs to be informed to the moc2. For this we need to make app register for the notification bcoz in all the cases moc posts notification **NSManagedObjectContextDidSaveNotification**. 

persistant stores that Core data provides :
- Sqlite
- In memory persistant store
- Binary store
- XML store

Core Data does not guarantee the security of the store from the untrusted sources.
Sqlite store offer better security then XML and binary store.

Concurrency is supported in the Core Data. 
Managed object context can be of 2 patterns : 
1. NSMainQueueConcurrencyType : It is used in main queue.
2. NSPrivateQueueConcurrencyType : It creates it seperate queue.

Here we can create private context using concurrency type : NSPrivateQueueConcurrencyType and it as child of main managed object context.
We can then perform the task inn private context and once done we can save it so that changes are reflected to main context.

To simplify this we can further use method of NSPersistanceContainer class.
let jsonArray = …
let container = self.persistentContainer
container.performBackgroundTask() { (context) in
    for jsonObject in jsonArray {
        let mo = EmployeeMO(context: context)
        mo.populateFromJSON(jsonObject)
    }
    do {
        try context.save()
    } catch {
        fatalError("Failure to save context: \(error)")
    }
}
Every time this method(**performBackgroundTask**) is invoked persistant container create new private context and execute the block passed in that queue.




