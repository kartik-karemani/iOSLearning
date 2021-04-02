
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
