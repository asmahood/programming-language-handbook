# Testing

Testing is accomplished in Java through **JUnit**. JUnit is a unit testing framework for Java that tests the functionality of an application to ensure it runs as expected. 

## JUnit Classes and Methods
JUnit testing takes place in a Java class. The functionality for those tests comes from JUnit classes, most commonly the `Assert` class and annotation classes. The four most essential annotations are `@Before`, `@Test`, `@After`, `@Ignore`. The above annotations can be imported in the following ways:
```java
import org.junit.Before;
import org.junit.Test;
import org.junit.After;
import org.junit.Ignore;
```
Additionally, the following line will grab all functionality from the `Assert` class library, but note that each assert method can be imported individually:
```java
import static org.junit.Assert.*;
```

## Creating a Test Method
To create a test method:
```java
@Test
public void test() {
    // Test Cases
}
```
These `@Test` annotated methods will always run unless otherwise annotated as `@Ignore`. These test methods also don't have to be called, as they're automatically detected and run by the compiler.


