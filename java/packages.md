# Packages

## Importing Packages
There are two ways to import a package in Java. The first way is to import the class itself.
```java
import java.util.ArrayList;
```
This style will make the class available for use and any static methods will be available using the class followed by the `.` operator.

The second way to import a package is to import all static methods into the global namespace.
```java
import static java.lang.Math.*;
```
Using this method, all static methods on the class will be available in the global namespace. So you would not need to specify the `Math` class to use them.
