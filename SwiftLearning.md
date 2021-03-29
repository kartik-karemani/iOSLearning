
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
