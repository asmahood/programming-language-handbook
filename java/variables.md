# Variables

## Variables 101
Notes:
- Variables can only start with a letter, `$`, or `_`

### Declaring a variable
Declaring a variable requires specifying the data type and name:
```java
datatype varName;
// Example
int age;
double salaryRequirement;
```

### Assigning a value to a variable
To assign a value to a variable, use the `=` operator
```java
varName = value;
// Example
age = 22
```

### Defining a variable
Defining a variable is declaring and assigning in one operation.
```java
datatype varName = value;
// Example
int age = 22;
```

## Data Types

### Primitive Data Types
| Data Type | Wrapper Class Name | Size (bits) | Default Value (for fields) | Description                                                |
|-----------|--------------------|-------------|----------------------------|------------------------------------------------------------|
| byte      | Byte | 8           | 0                          | Represents whole numbers ranging from -128 to 127          |
| short     | Short | 16          | 0                          | Stores smaller whole numbers from -2^15 to 2^15 - 1        |
| int       | Integer | 32          | 0                          | Represents whole numbers from -2^31 to 2^31 - 1            |
| long      | Long | 64          | 0L                         | Represents very large whole numbers from -2^63 to 2^63 - 1 |
| float     | Float | 32          | 0.0f                       | Stores floating point numbers with 7 digits of precision   |
| double    | Double | 64          | 0.0d                       | Stores floating point numbers with 15 digits of precision  |
| boolean   | Boolean | N/A         | false                      | Holds either `true` or `false`                             |
| char      | Character | 16          | '\u0000'                   | Stores a single character, including letters and ASCII     |

### Reference/Object Data Types
Objects are data types that have built-in behaviour.

## Constant Variables
To declare a variable with a value that cannot be manipulated (constant), use the `final` keyword as so.
```java
final int yearBorn = 1968;
```
Attempting to change this variable will give the following error
```
error: cannot assign a value to final variable yearBorn
```

## Type Casting
If you want to cast from one type to another, you need to use the casting operator `(type)`. For example:
```java
int b = (int)(Math.random() * 10);
```
This will cast the `double` value returned by `Math.random()` to an `int`.
