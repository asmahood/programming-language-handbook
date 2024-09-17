# Strings
`String` is a class that holds a sequence of characters. Strings can be created in two ways:
- Using a literal: `String greeting = "hello world";`
- Calling the constructor of the string class: `String greeting = new String("Hello world");`

## Checking Equality
Strings cannot be compared using the `==` operator. Objects must be compared using a `.equals()` method. For example
```java
String person1 = "Paul";
String person2 = "John";

System.out.println(person1.equals("John")) // #=> false
System.out.println(person1.equals("Paul")) // #=> true
```

## Combining Strings Together
Two strings can be concatenated together using the `+` operator. For example:
```java
String username = "PrinceNelson";
System.out.println("Your username is: " + username); // #=> "Your username is PrinceNelson"
```
You can also use a primitive datatype as the RHS of the `+` operator and it will implicitly converted to a `String`.
