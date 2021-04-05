
var - It is used for the variables. We can change the value once its initialized.
let - It is used for the constants. Once initialized we cannot change its value.

Booleans Type : It can have only 2 values i.e. True or False. Example:
**let trueValue = true
let falseValue = false**

**let passingGrade = 50
let studentGrade = 74
let studentPassed = studentGrade > passingGrade**

Comparison operator - Used to compare 2 values.
**let samGrade = 49
let chrisGrade = 99
samGrade == chrisGrade
samGrade != chrisGrade**

Logical Operator:
1. NOT operator - Returrns the inverse of the bool value. !
2. AND operator - &&. Returns true if both the operands are true else it will return false.
3. OR operator -  Return true if any one of the operand is true. ||

IF-ELSE : It is used to execute a set of statements based on some condition :
**if studentPassed {
    print("Congrats")
}else{
    print("Keep studying")
}**

Ternary Operator : Here an expression is checked. Then value is set based on that.
**let betterStudent = studentPassed ? "YES":"NO"**

Optionals: Marking a type as options represents that it can have value or cannot have a value. 
**let betterStudent = studentPassed ? "YES":"NO"


Dictionary:
It is an unordered collection type. It stores the data in key value pair. keys in the dictionary should be unique.
**var emptyDictionary : [String:Int] = [:]
var namesAndPet = ["a":"A","b":"B"]**

Iterating through dictionary values:
**for (keyInfo,valueInfo) in namesAndPet {
    print("key is :\(keyInfo) and value is : \(valueInfo)")
}**


var petName:String?
petName = "Mango"
print(petName)**

Forced unwrapping optional:
**print(petName!)** - This is not a recomended way to unwrap the optionals as it may lead to crash the app in case the petName is nil. 
Use forced unwrapping only if you know the option is having a value.

Optional Binding: - Way to safely unwrap the optional.
**if let petName = petName {
    print("Name of the pet is \(petName)")
}**

Nil Coalescing Operator:
It is used to unwrap the optional. In case the value of optional returns nil then it will return a default value. For ex :
**let optionalInt : Int? = nil
let requiredInt = optionalInt ?? 0**

Collections:
Tuples: In iOS we can store the related data as a single unit using Tuples. For example in case to store the location we need to store both longitude and latitude.
**let location : (lat:CGFloat,long:CGFloat) = (100.0,200.0)
location.lat
location.long**
Now this constant is having 2 pieces of information.
**let (anotherLocLat,anotherLocLong) = location
anotherLocLat
anotherLocLong**

Arrays:
It is used to store the elements of same type.
These are ordered type.Each element in array can be accessed using index.
**let pastries : [String] = ["cookie","cupcake","donut"]**

**var pastriesVar : [String] = []
pastriesVar.append("abcd")
pastriesVar.append("gggg")**

We can fetch the elements from an array using the index.
**pastriesVar[0]**

Different operations on array :
1. count - To get the count of the array
2. isEmpty - Check if array is empty
3. contains - Check if array contains a particular element or no

Control Flows:
while Loop : Here a set of statements are executed till a condition evalutes to true. Here condition is evaluated first and if its true then set of statements are executed.
**var index = 1
while index < 10 {
    print(index)
    index += 1
}
**

Repeat while example: It is going to execute the statement at least once. Here condition is evaluated after statements are executed.
**index = 1
repeat {
    print(index)
    index += 1
}while(index<10)**

For Loop: Here we are executing a set of statement for particular number of times.
**for i in 0...5 {
    print(i)
}
**
**for _ in 0...5 {
    print("testing")
}**

Iterating over collection:
For loop can be used to iterate over a collection.
**let days = ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"]
for day in days {
    print(day)
}**

break : We can use break statement to exit from the loop based on some condition.
**let days = ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"]
for day in days {
    if day == "Thursday" {
        break
    }
    print(day)
}**
continue : If we dont want to execute some statement for some elements while iterating the collection we can use continue.
**let days = ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"]
for day in days {
    if day == "Thursday" {
        continue
    }
    print(day)
}**

Sets: It is unordered collection of values with same data type. It contains the unique value. We can compare the different sets.
**var setObj : Set<Int> = [1,2,3,4,5,1]
print(setObj)
setObj.contains(3)
setObj.contains(444)
setObj.count
setObj.insert(333)
print(setObj)**
    

1. Named Types and Compund Types
 Named Types : Classes , Structure, Enum and protocol
 Compund Types : Tuples, Functions.
2. Reference and Value types

Function : 
Functions in swift perform some task. It can reused across app by calling it thus avoiding the duplication.
**func sayHello() {
    print("Hello !!!")
}
sayHello()**
Functions with parameters:
**func sayHello(msg:String) {
    print(msg)
}
sayHello(msg: "Hello Everyone !!!")**

We can also set the default values for the function parameter.

Function returning a value:
**func sayHelloMessageFunction(msg:String) -> String {
    return "Hello \(msg)"
}
print(sayHelloMessageFunction(msg: "Peter"))**  

Structure:
Structure is a type used to encapsulate the related data together. It defines the properties and methods as well.
Structure automatically generates the initializer.
When a method defined in the structure tries to mutate the structure properety then it should be explicitly declared as mutating.
If structure type is assigned to a constant then it cannot mutate the structure property.
If structure type is assigned to a variable then it can mutate the structure property.
Structure is a value type.

**struct Student {
    let name:String
    var grade:Int
    var pet:String?
    func getPassStatus(lowestPass:Int = 50) -> Bool {
        return grade >= lowestPass
    }
    mutating func addBonus(){
        grade += 5
    }
}
var kartik = Student(name: "kartik", grade: 75, pet: nil)
kartik.getPassStatus()
kartik.grade = 50
kartik.grade**

Classes:
Classes are similar to that of structure i.e. they have properties,methods and initializers but they are reference types.
Classes do not get automatic generated initializer that structs do.

Function overloading : Creating multiple function with same name but different signature is called Function overloading. Like function with same name can have different number of parameters, different parameter types, return types.

Ex:
**func printMessage(message:String) {
    print(message)
}
func printMessage(message1:String,message2:String){
    print(message1+message2)
}
printMessage(message: "Hello World")
printMessage(message1: "Hello", message2: "Everybody")**

Variadic parameters : The parameter list varies here. Like 0 to more then 0 number of input paramters.
The below method accepts 0 or more number of ints and return an int value. variadic paramter is considered as an array inside the function.
**func highestGrade(grade:Int...) -> Int {
    grade.max() ?? 0
}
highestGrade(grade: 1,2,3,4,45)**

inout keyword: Function cannot changes the parameters inside the body. For this parameter should be declared as inout keyword.
**var countInfo = 0
func incrementAndPrint(_ value: inout Int) {
    value += 1
    print(value)
}
incrementAndPrint(&countInfo)
incrementAndPrint(&countInfo)
incrementAndPrint(&countInfo)
incrementAndPrint(&countInfo)
countInfo**

Functions in the swift are just data type. They can be stored in a variable or constants or passed to a function.
**func printResult(_ operate:(Int,Int)->Int,_ a:Int, _ b: Int) {
    let result = operate(a,b)
    print(result)
}


**func add(number1:Int,number2:Int)->Int{
    number1+number2
    
}**
**var function = add
printResult(function, 1, 1)
function(5,5)
func subtract(number1:Int,number2:Int)->Int{
    number1-number2
    
}
**function = subtract
printResult(function, 5, 1)******
function(4,2)

Such function using another function as a parameter is called higher order function.

Closures:
It is a block of code used to perform some task. It can be stored in constant or variable or can be passed to some functions. Closure doesnot have name as of functions.We cannot argument label in Closure as compared to the functions.
**var addClosure = { (a:Int,b:Int)->Int in
    a+b
}
let res = addClosure(1,2)**


Functions VS Closure:

1. Function have names whereas Closure doesnot have name.
2. Function have argument labels whereas it is not allowed in closures
3. Function have default values for the parameter whereas it is not allowed in the closure.

When we call a function that accepts the closure as last parameter we can use trailing closure syntax.


forEach:Used to iterate over a collection. For EX:
**let prices = [100,200,300,400,500]
prices.forEach { (price) in
    print(price)
}**

map :If we have to perform some operations on all the elements of the array then we can use the map function.
**let updatedPrice = prices.map { (price) -> Int in
    return price*2
}
updatedPrice**

compactMap: It is used to perform some operation on all elements of the collection. It will add only the resultant data which is not nil.
**let inputArray = ["1","2","Strinhhg"]
let outPutArray = inputArray.compactMap { Int($0) }
outPutArray**

flatMap: If we have collection with in the collection, then it is used to convert that in a single collection.
**let words = [["a","b","c"],["d","e","f"]]
let resultData = words.flatMap { (data) -> [String] in
    return data
}
resultData**

filter : We can filter the collection based on the criteria.
**let dataInfo = [1,2,3,4,5]
let result = dataInfo.filter { (data) -> Bool in
    data > 2
}
result**

Sort:Used to sort the collection.
**let sortedData = dataInfo.sorted { (a, b) -> Bool in
    return a>b
}
sortedData**


Properties:
Stored Property : It is used to store a value.
**struct Wizard {
    var firstName:String
    var lastName:String
}
let wizard = Wizard(firstName: "Kartik", lastName: "Karemani")
wizard.firstName
wizard.lastName**
Here firstName and lastName are the stored property.
Property Observers are something which is called everytime the property is set. i.e willSet(Called before property is set) and didSet(Called after property is set).
**struct Wizard {
    var firstName:String {
        willSet{
            print(firstName + "will be set to " + newValue)
        }
        didSet {
            if firstName.contains(" ") {
                print("No Space allowed!!!!")
                firstName = oldValue
            }
        }
    }
    var lastName:String
}**

Type properties : These properties belongs to the type instead of instance. Means for all the instance of the instance type property is common.
**struct Wizard {
    static let wizardCommonInfo = "Wizard information"
    var firstName:String {
        willSet{
            print(firstName + "will be set to " + newValue)
        }
        didSet {
            if firstName.contains(" ") {
                print("No Space allowed!!!!")
                firstName = oldValue
            }
        }
    }
    var lastName:String
}
Wizard.wizardCommonInfo**

Computed Property : This calculates the value everytime it is accessed.
**struct Employee{
    var firstName:String
    var lastName:String
    var fullName:String{
        return firstName+" "+lastName
    }
}
var emp = Employee(firstName: "Kartik", lastName: "Karemani")
emp.fullName**

Lazy stored properties are not created during initialization and instead they are created when they are invoked.
Methods are similar to functions but they reside inside a class or a structure.
Class Methods belongs to type rather then the instance of the type.


Inheritance:
Here subclass inherits the features from the base class like properties, methods and initializers.
Protocol are the set of rules which an object needs to define inorder to confirm it.
**class Student : Person {
    var grades : [Int] = []
}
var student = Student(firstName: "Kartik", lastName: "Karemani")
student.firstName
student.lastName
student.grades
student.grades = [100,200,300,400,500]
student.grades**

In swift a class can have only one base class. Here student is person. so it cannot inherit from other class. Multiple inheritance is allowed in swift.

Polymorphism : Based on the context a subclass can be treated as its own type or any of the superclass.
You cannot override computed property with a stored property but other way is fine.

Swift have requirement tht all stored properties should have initial values.
A child class needs to first initialize its stored properties then invoke initializers for its super class.
We can declare an initializer as required due to which all the subclasses needs to implement that initializer.

Designated initializers initialize the stored property of its class and up the hierarcy
whereas convenience initializers delegates this task to the designated initializers with setting some of the parameters to default value.

A designated initializer must call a designated initializer from its immediate superclass.
Convenience initializer must call another initializer from same class. i.e it should ulitmately call a designated initializers.

Protocols:
Protocols are the set of properties, methods that represents a requirement. 
Any class, structure or enum defining those requirement is said to confirm the protocol.

**protocol Animal {
    var name : String { get }
}**
Protocols includes only declaration and not definition.
Protocol can inerit from other protocol.

Extension : It is used to extend the functionality of class, struct or enum by adding the methods,properties and initializers.
it can be used to provide default implementation for the protocol methods.
We cannot add designated initializer and stored property in the extension.

Error Handling : It is process of handling error occuring in the code.
Failable initializder: It can be used for handling error. initializer can return nil if passed input parameter are not valid. For Ex:
**struct Email {
    var address:String
    init?(emailAddress:String) {
        guard emailAddress.contains("@") else {
            return nil
        }
        self.address = emailAddress
    }
}
let emailKartik = Email(emailAddress: "Kartik@gmail.com")
let emailIshan = Email(emailAddress: "Ishan")
if let _ = emailKartik {
    print("Kartik -Object created")
}else{
    print("Kartik -Object Not created")
}
if let _ = emailIshan{
    print("Object created")
}else{
    print("Object Not created")
}**

Another way of handling error : Error object in iOS confirms to Error protocol.Function can throw error. It should be called in do catch block.
Example :
**enum MathError:Error{
    case DiveByZeroError
}
func divide(numnerator:Double,denominator:Double) throws -> Double {
    if denominator == 0 {
        throw MathError.DiveByZeroError
    }else{
        return numnerator/denominator
    }
}
do {
    let result = try divide(numnerator: 10, denominator: 0)
    print(result)
} catch {
    dump(error)
}**

For error handling we can also use Return type. It is a type which has info : success or failure and associated object with it.
**enum MathErrorInfo:Error{
    case DiveByZeroError
}
func divideFunc(numnerator:Double,denominator:Double) -> Result<Double,MathErrorInfo> {
    if denominator == 0 {
        return .failure(MathErrorInfo.DiveByZeroError)
    }else{
        return .success(numnerator/denominator)
    }
}
let res = divideFunc(numnerator: 10, denominator: 0)
switch res {
case .success(let val):
    print(val)
case .failure(let error):
    print(error)
}**


Values - Isolation
Reference - Shared Ownership
Swift Types :
1. Named : Class, struct, enum and protocol
2. Compund : Function and Tuple

Diff between Value and Reference Type ----
If value type is assined to other variable then changing that variable is not going to effect the original data since is copied where as if referece type like class object is assigned to other variable and something is changed then it is reflected in the original data as well.

To mutate the function parameter from with in the function it needs to be marked with inout keyword.
If method present in value type wants to mutate the property it needs to be marked as mutating.

Methods in class ,enums and struct are passed self paramter. But a method marked as mutating it is passed with inout keyword.

COW : Copy on write ------- Need to study deep
If their are 2 reference to ABCD class i.e obj1 and obj2.
Making change in obj1 will effect obj2 as well. To protect before  writing obj1 can create copy of ABCD object. This is called copy on write


Generics:
Generics is used to create reusable function, type that can be used for other types as well. For ex : if method add acceepts 2 int and adds them and return int
to add 2 doubles we need to create one more method. instead if we can make add method generic then it will accept other type as well. Example of generic is swift array.
We can write generic Function, initializer, class, struct and enum

**struct Stack<Element> {
    var storage : [Element] = []
    
    mutating func push(element:Element) {
        storage.append(element)
    }
    
    mutating func pop() -> Element? {
        return storage.popLast()
    }
    
    var top : Element? {
        return storage.last
    }
    
    var isEmpty : Bool {
        return top == nil
    }
}
var stack = Stack<Int>()
stack.push(element: 23)
stack.push(element: 24)
stack.top**
    
Here <Element> indicates placeholder type Element. It is replaced by actual type during the initialization.

Genenric Constraint : Here we can add constraint to the placeholder type so when actual type is given while creating instance then if actual type shhould satisfy the constraint.
**func add<Element:Numeric>(a:Element,b:Element) -> Element {
    return a+b
}
add(a: 55, b: 55)**

Associated Types: These are used to make the protocol generic.
protocol Persistable {
    associatedtype Entity : NSManagedObject
    func create(entity:Entity)
    func read(entity:Entity)
    func update(entity:Entity)
    func delete(entity:Entity)
}

struct EmployeeEntity : Persistable {
    typealias Entity = Employee
    
    func create(entity:Employee) {
        
    }
    func read(entity:Employee) {
        
    }
    func update(entity:Employee) {
        
    }
    func delete(entity:Employee){
        
    }
}
Here Persistable is a generic protocol created using associated type. All the methods take input of type Entity which is constrained to be of type NSManagedOBject.
EmployeeEntity confirms thihs protocl. It infers entity as employee.


Conditional Conformance :
In below code Pair is equatable only if Element is equatable. This is called as conditional conformance.
struct Pair<Element> {
    var firstName:Element
    var lastName :Element
}
extension Pair : Equatable where Element : Equatable {
    
}

**Automatic Reference Counting(ARC):**
ARC is used in iOS to perform the memory management. It manages the memory based on the object ownership. As long as object is needed it statys in the memory but when its no longer needed it is deallocated from the memory.
An object will stay in the memory as long as their is at least one strong reference to that object i.e. when reference count is greater than zero.

**Strong Reference Cycle:**
Suppose their are 2 classses Person and Apartment. Instance of Person is stored in john(john is having strong reference to Person) and instance of Apartment is stored in unitA(unitA is hhaving a strong reference to the Apartment). Along with these if Person and Apartment have strong reference to each other. In this case even if we make below objects nil 
john = nil
unitA = nil
Both Person and Apartment are not going to deallocate from the memory and they cant be accessed leading to memory leak.
All the weak reference to an object becomes nil when it is deallocated.

Resolving the issue:
One of the property needs to be declared as weak to resolve strong reference cycle issue.
Use unowned reference only when refernce always refers to instance. ARC will not make unowned reference nil when object is deallocated

Strong reference cycle also occurs when you assign closure to class property and body of the closure captures the instance.
It can be avoided using closure capture list.
A capture list can be defined during the closures definition. It defines the rules to capture the reference in the closure body

Optional Chaining:
Optional chaining is process of calling the property or functiona on the option value. It might be nil. In case it has value then call to property or method is success or else call will return nil value.
Since the result of the optional chaining can be nil value so result is an option even if property we are accessing is non optional.
class Person {
    var residence: Residence?
}
class Residence {
    var numberOfRooms = 1
}
**let john = Person()
if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
// Prints "Unable to retrieve the number of rooms."**
john.residence = Residence()
**if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
// Prints "John's residence has 1 room(s)."**

During a optional chaining the type of value we are trying to retrieve will become optional bcoz of optional chaining.

**Conflicting access to the memory : Here same memory location is accessed from mulitple places at the same time.(i.e both read and write operation which corrupts the data)** For ex below:
**var stepSize = 1

func increment(_ number: inout Int) {
    number += stepSize
}
increment(&stepSize)**
Here read access of stepSize conflicts with write acces for number.

