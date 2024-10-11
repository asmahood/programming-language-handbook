# Getting Started
Java is a complied object-oriented language. In Java, all code must be placed inside a class. Some things to remember:
- A Java class must be saved in a file that has the exact same name as the class.
- Classes can have any name as long as it doesn't start with a number.
- Convention is that Java classes start with a capital letter.

## JDK and JRE, and other flavours of Java
The Java Development Kit (JDK) contains the tools required to compile and run a Java application.

The Java Runtime Environment (JRE) is a subset of the JDK and only contains the tools needed to run a Java application. You cannot compile with the tools in the JRE.

There are other versions of Java such as J2EE, Java EE, or Jakarta EE which all refer to the Java Enterprise Edition. This is a set of tools and libraries to create entreprise-class applications. 

## Writing a Java program

### Creating the main Java class
To start a java program, create a new file called `<ClassName>.java`, for example `MyClass.java`. Inside this file, write

```java
public class MyClass {
  public static void main(String... args) {
    System.out.println("Hello World!");
  }
}
```

## Compiling and running a Java application
### Compiling
To compile a Java file, run
```bash
javac MyClass.java
```

### Running a Java Application
After compiling, you can run the file by using the command

```bash
java MyClass
```

To pass arguments, add them after the name of the class.
```bash
java MyClass Arg1
```

Since Java SE 11, you can run a Java application without compiling as long as the program is a single file. Using the command

```bash
java MyClass.java
```

#### Running a Java Application with Multiple Files
You must compile all files as so:
```bash
javac TransportBike.java
javac TransportCar.java
javac TransportationDriver.java

# OR

javac TransportBike.java TransportCar.java TransportationDriver.java

# OR

javac Transport*.java
```
Another method is to compile the file with the main class
```bash
javac TransportationDriver.java
```
This works because as the compiler reaches a definition that is unknown to it, such as the first instance of `TransportBike`, it will search the current folder for any `.class` files that match that signature. If no `.class` files are found, it will look for `.java` files and then attempt to compile them so that it knows how to represent the TransportBike object.

## Java Syntax

### Comments
To start a single comment, use `//`:
```java
// This is a single line comment
```

For multi-line comments, use `/* <text> */`
```java
/* 
This is a multi-line
Java comment.
*/
```

To create documentation for Java code, use a Javadoc comment `/** *<text> */`. They are written before declaration of fields, methods, and classes. 
```java
/**
* This a Javadoc comment
*/
```

### Whitespace
Java does not interpret whitespace, so the following two codeblocks are equivalent:
```java
System.out.println("Java");System.out.println("Lava");System.out.println("Guava");
```
```java
System.out.println("Java");

System.out.println("Lava");

System.out.println("Guava");
```

### Semicolons
Semicolons are required at the end of a statement. 

### Scope
Curly braces (`{}`) mark the scope of classes and methods. Semicolons are not required at the end of braces.
