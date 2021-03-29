
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
