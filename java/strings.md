# Strings
`String` is a class that holds a sequence of characters. Strings can be created in two ways:
- Using a literal: `String greeting = "hello world";`
- Calling the constructor of the string class: `String greeting = new String("Hello world");`
Strings in Java are immutable, so they cannot be changed.

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

## String Methods

### length
The `length()` method returns the length (total number of characters) in the string.
```java
String str = "Hello world!";
System.out.println(str.length()) // 12
```

### concat
The `concat()` method concatenates one string to the end of another string.
```java
String str1 = "Hello ";
String str2 = "World!";

str1 = str1.concat(str2);

System.out.println(str1); // Hello World!
```
Since `str1` is a reference to a `String` object, when `concat()` is called, we change its value to reference a new `String` object.
If you do not reassign the value, `str1` would remain the same.

### equalsIgnoreCase
The `equalsIgnoreCase()` method is similar to the `equals()` method, except it ignores casing in the strings.

### compareTo
The `compareTo()` method is used to lexicographically compare two `String`'s. The output is an `int` that represents the `difference` between the two `String`'s.
```java
String flavor1 = "Mango";
String flavor2 = "Peach";

System.out.println(flavor1.compareTo(flavor2)); // #=> -3
```
If the return value is:
- `0`: the two strings are equal
- `< 0`: then the `String` object is lexicographically less than the `String` argument
- `> 0`: then the `String` object is lexicographically greater than the `String` argument

Note that this does not ignore casing, so `Mango < Peach`, however `mango > Peach` since the Unicode value for `m` is larger than `P`.

### compareToIgnoreCase
This method is similar to `compareTo` except it ignores casing.

### indexOf
The `indexOf()` method returns the index of the first occurence of a character or substring in a string.
```java
String letters = "ABCDEFGHIJKLMN";

System.out.println(letters.indexOf("C")); // #=> 2
System.out.println(letters.indexOf("EFG")); // #=> 4
```

### charAt
The `charAt()` method returns the character located at a specifed index. If the index is greater than or equal to the strings length, an `StringIndexOutOfBoundsException` error is thrown.
```java
String str = "qwer";

System.out.println(str.charAt(2)); // #=> "e"
```

### substring
The `substring()` method extracts a part of the string and returns a new `String` with this slice. It takes a starting index, and optionally an ending index. The starting index is **inclusive** and the ending index is **exclusive** (the character at the ending index will not be included).
```java
String line = "The Heav'ns and all the Constellations rung";

System.out.println(line.substring(24)); // #=> "Constellations rung"
```

### toUpperCase
The `toUpperCase()` method returns a new `String` with all characters converted to uppercase.
```java
String input = "Cricket!";

String upper = input.toUpperCase(); // #=> "CRICKET!"
```

### toLowerCase
The `toLowerCase()` method returns a new `String` with all the characters converted to lowercase
```java
String input = "Cricket!";

String upper = input.toLowerCase(); // #=> "cricket!"
```
