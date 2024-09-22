# Operators

The available operators in Java are:

## Arithmetic Operators

| Operator Name | Symbol | Example | Description |
|---------------|:------:|---------|-------------|
| Addition      | +      | `a + b` | Adds two variables together using addition |
| Subtraction   | -      | `a - b` | Subtracts two variables |
| Increment     | ++     | `a++`   | Increases the value of a number by 1 |
| Decrement     | --     | `a--`   | Decreases the value of a number by 1 |
| Multiplication| *      | `a * b` | Multiplies two numbers together |
| Division      | /      | `a / b` | Divides two numbers together. **Note: dividing integers will do integer divison (result will be floored)** |
| Modulo        | %      | `a % b` | Gives the remainder after two numbers are divided |
| Compount Assignment | (+-*/%)= | `a += b` | Performs the arithmetic expression and then reassigns the value to the LHS to the result |

### Order of Operations
The order of operations for arithmetic operators is defined below. Operators that share the same precedence are evaluated from Left-to-Right within the expression.
1. Parentheses
2. Exponents
3. Modulo/Multiplication/Division
4. Addition/Subtraction

## Relational Operators

| Operator Name | Symbol | Example | Description |
|---------------|:------:|---------|-------------|
| Greater Than  | \>      | `a > b` | Check if one value is greater than another |
| Less Than     | \<     | `a < b` | Check if one value is less than another |
| Equals        | ==     | `a == b`| Check if two values are equal |
| Not Equals    | !=     | `a != b`| Check if two values are not equal |
| Greater Than Or Equal To | \>= | `a >= b` | Check if one value is greater than or equal to another value |
| Less Than Or Equal To | \<= | `a <= b` | Check if one value is less than or equal to another value |

*Note: equality of objects cannot be checked using the `==` operator. To compare objects, use the `.equals()` method.*

## Conditional Operators

| Operator Name | Symbol | Example | Description |
|---------------|:------:|---------|-------------|
| AND           | &&     | a && b  | Evaluates to true if both `a` and `b` are true, otherwise it evaluates to false |
| OR            | ||     | a || b  | Evaluates to true if either `a` or `b` are true, otherwise it evaluates to false |
| NOT           | !      | !a      | Evluates to true if `a` is false, and false if `a` is true |

You can control the evaluation of conditions by surrounding them in `()`. Conditions in `()` will be evaluated first.
