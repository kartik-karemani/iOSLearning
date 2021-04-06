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
