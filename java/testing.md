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

## @Test
To create a test method:
```java
@Test
public void test() {
    // Test Cases
}
```
These `@Test` annotated methods will always run unless otherwise annotated as `@Ignore`. These test methods also don't have to be called, as they're automatically detected and run by the compiler.

### Assertions
Assertions are found in the `junit.org.Assert` package. Below are a couple of common assert methods *(note that they all have a return type of `void`)*:

| Assert Method | Description |
| ------------- | ----------- |
| `assertEquals(expected, actual)` | Checks if two values are equal |
| `assertNotEquals(expected, actual)` | Checks if two values are not equal |
| `assertTrue(boolean)` | Checks if a condition is `true` |
| `assertFalse(boolean)` | Checks if a condition is `false` |
| `assertNotNull(object)` | Checks if an object isn't `null` |
| `assertNull(object)` | Checks if an object is `null` |
| `assertArrayEquals(expectedArray, actualArray)` | Checks if two arrays are equal |

## @Ignore
The `@Ignore` annotation will prevent a test from running. 

*Note: in JUnit 5, this annotation is called `@Disabled`*.

## @Before
Methods tagged with `@Before` will run before each test method:
```java
@Before
public void beforeEachTest() {
    // Something multiple tests use
}
```
*Note: In JUnit 5, this is called `@BeforeEach`*

## @BeforeClass
Methods tagged with `@BeforeClass` will run before all tests instead of multiple times:
```java
@BeforeClass
public void beforeAllTests() {
    // Something all tests use
}
```
*Note: in JUnit 5, this is called `@BeforeAll`*.

## @After
Methods tagged with `@After` will reun after each test method:
```java
@After
public void afterEachTest() {
    // Cleanup
}
```
*Note: In JUnit 5, this is called `@AfterEach`*

## @AfterClass
Methods tagged with `@AfterClass` will run only once after all tests conclude:
```java
@AfterClass
public void afterAllTests() {
    // Cleanup
}
```
*Note: in JUnit 5, this is called `@AfterAll`*

## @Suite
The `@Suite` annotation is used to organize tests into test suites. A test suite is a way to bundle JUnit test classes and run them together. The `@RunWith` and `@Suite` annotations accomplish this:
```java
@RunWith(Suite.class)
@Suite.SuiteClasses({
  // List of test classes to bundle together
})

public class MyTestSuite {
}
```
The `MyTestSuite` class doesn't need anything within the class itself to run. It instead will be called by a runner class:
```java
import org.junit.runner.JUnitCore;
import org.junit.runner.Result;
import org.junit.runner.notification.Failure;

public class TestSuiteRunner {
  public static void main(String [] args) {
    Result result = JUnitCore.runClasses(MyTestSuite.class);

    for (Failure failure : result.getFailures()) {
      System.out.println(failure.toString());
    }

    System.out.println(result.wasSuccessful());
  }
}
```
With a test suite, one environment can be created and all of the test classes can interact with it accordingly. The last test class bundled into the suite can then handle the cleanup.

## @TestFactory
*Available in JUnit 5.*

Methods annotated with `@TestFactory` provide a test factory for dynamic tests.

## @Nested
*Available in JUnit 5.*

Methods annotated with `@Nested` denoted nested tests.

## @Category
Methods tagged with `@Category` are used for tagging and filtering.

*Note: In JUnit 5, this is called `@Tag`*.

## @ExtendedWith
*Available in JUnit 5.*

Methods tagged with `@ExtendedWith` allow you to register custom extensions.

## Assumptions
JUnit 4 supports five `org.junit.Assume` methods:
- `assumeFalse()`
- `assumeNoException()`
- `assumeNotNull()`
- `assumeThat()`
- `assumeTrue()`


## JUnit 5
In JUnit 5, `Assert` was renamed to `Assertions` and added `assertThrows` and `assertAll` methods. Additionally, this added new overloaded methods:
```java
public static void assertEquals(long expected, long actual)
public static void assertEquals(long expected, long actual, String message)
public static void assertEquals(long expected, long actual, Supplier messageSupplier)
```

JUnit 5 changed this to now allow them to be package protected and private. It does this by using reflection. This also extends to constructors that allow arguments now.

### Assumptions
In JUnit 5, three assumptions are supported:
- `assumeFalse()`
- `assumeThat()`
- `assumeTrue()`

### Test Suites
Test suites in JUnit 5 are created like so:
```java
import org.junit.platform.runner.JUnitPlatform;
import org.junit.platform.suite.api.SelectPackages;
import org.junit.runner.RunWith;

@Suite
@SelectPackages("com.package.path")
```
