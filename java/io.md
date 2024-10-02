# Input and Output

## Printing to the Standard Output
To print to the console (standard output), we use the `System.out` class which is an instance of a `PrintStream`. 
To print one line at a time:
```java
System.out.println("string");
```
Note that this will start whereever the programs "cursor" currently is and add a newline character at the end.

To print without starting a new line:
```java
System.out.print("string");
```
Note that this will leave the cursor at the end of the character 'g', so any subsequent prints will start after.

To output strings that are formatted in code we use:
```java
System.out.printf("Hello %s", "World");
```
This uses [format specifiers](https://docs.oracle.com/javase/9/docs/api/java/util/Formatter.html#syntax) that begin with `%` followed by the type of the variable we want to print.

## Reading User Input
The `Scanner` class is used to read user input into a Java program. We read the user input from the `System.in` class which represents input from the standard input and is an instance of a `InputStream`. To use the `Scanner` class, we must import it:
```java
import java.util.Scanner;
```
To create an instance of a new scanner class:
```java
Scanner input = new Scanner(System.in);
```

### Reading Data

The `Scanner` breaks up its input using a defined delimiter and by default it is set to whitespace. Also note that the `Scanner` class is blocking, meaning it will wait for user input and block execution of the program until it gets provided. To read some bit of information requires specific methods depending on the type of information you are looking for:

| Variable | Code |
| -------- | ---- |
| String | `String myString = input.next()` |
| Int | `int myInt = input.nextInt()` |
| Double | `dobule myDouble = input.nextDouble()` |
| Byte | `byte myByte = input.nextByte()` |
| Boolean | `boolean myBool = input.nextBoolean()` |
| Long | `long myLong = input.nextLong()` |
| Short | `short myShort = input.nextShort()` |

### Validation and Control Flow
The `Scanner` class also has several methods that help support data validation and control flow:
| Code | Description |
| ---- | ----------- |
| `input.hasNext()` | This function returns a boolean that indicates if there is another token left to process |
| `input.hasNextLine()` | This function returns a boolean that indicates if there is another line in the input of the defined scanner. |
| `input.hasNextInt()` | This function returns a boolean that validates if there is another int in the input of the defined scanner. |
| `input.useDelimiter(",")` | This function helps us specify what delimiters we want to use. A delimiter is used to separate data units. This , delimiter can be especially useful when a program is required to read csv (comma separated values) files. |

## Working With Files
When working with external files, `FileReader` and `FileWriter` are two extremely useful classes. To use these classes, we need to import them:
```java
import java.io.FileReader;
import java.io.FileWriter;
```
Note that these classes will throw a `IOException` which also needs to be imported. To declare that a method throws an error:
```java
public static void main (String[] args) throws IOException {}
```
If the errors are handled in a `try-catch` block, you do not need to add this to the declaration.

### Reading Files

To create a new `FileReader` instance, supply a file path (absolute or relative) in the constructor:
```java
FileReader reader = new FileReader(filePath);
```
Another option is to create a new `File` instance and pass this into the constructor of `FileReader`:
```java
File inputFile = new File(fileName);
// Pass File object to FileReader
FileReader input2 = new FileReader(inputFile);
```

#### Reading Data
Like `Scanner`, `FileReader` also has methods to validate and read content from files:
| Code | Description |
| ---- | ----------- |
| `inputFile.ready()` | Returns true if there is content to read |
| `inputFile.read()` | Reads the file one character at a time |

### Writing to Files
To create a new `FileWriter` instance:
```java
FileWriter output = new FileWriter(outputPath);
```
This will create a file with the name of the value of `outputPath`. This will not create directories only the file. If the directory does not exist, a `FileNotFoundException` will be thrown, which is a subclass of `IOException`. Alternatively you can create a `File` object to pass into the `FileWriter` constructor:
```java
File outputFile = new File(fileName);
// Pass File object to FileWriter
FileWriter output2 = new FileWriter(outputFile);
```

#### Writing Data
To write data to a file, you use the `write` method on the `FileWriter` class. It accepts a `String` as an argument.
```java
// Declare statement
String statement = "Hello World!";

// Option 1:
// Write all contents to file
output.write(statement);

// Option 2:
// If you want to write specific portions of a string to a file you may choose to use the following statement
// output.write(String str, int offset, int length);
output.write(statement, 0, 5);
// Writes only "Hello" to the file
```




### Closing Files
It is extremely important to close resources such as files and input streams as these tie up memory on the processor and in some file systems only one asset can access a file at a time. Resources can either manually be closed using a method or automatically using the `try-with-resources` block. For example:
```java
// Close a file manually
file.close();

// ==== OR ====


```

