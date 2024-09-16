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
| Data Type | Size (bits) | Default Value (for fields) | Description                                                |
|-----------|-------------|----------------------------|------------------------------------------------------------|
| byte      | 8           | 0                          | Represents whole numbers ranging from -128 to 127          |
| short     | 16          | 0                          | Stores smaller whole numbers from -2^15 to 2^15 - 1        |
| int       | 32          | 0                          | Represents whole numbers from -2^31 to 2^31 - 1            |
| long      | 64          | 0L                         | Represents very large whole numbers from -2^63 to 2^63 - 1 |
| float     | 32          | 0.0f                       | Stores floating point numbers with 7 digits of precision   |
| double    | 64          | 0.0d                       | Stores floating point numbers with 15 digits of precision  |
| boolean   | N/A         | false                      | Holds either `true` or `false`                             |
| char      | 16          | '\u0000'                   | Stores a single character, including letters and ASCII     |
|-----------|-------------|----------------------------|------------------------------------------------------------|

### Reference/Object Data Types
Objects are data types that have built-in behaviour.

#### String
Hold a sequence of characters. Can be created in two ways:
- Using a literal: `String greeting = "hello world";`
- Calling the constructor of the string class: `String greeting = new String("Hello world");`

