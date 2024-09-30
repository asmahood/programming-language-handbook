# Errors

## Exception Handling

One way to handle exceptions is by using `try`/`catch`. The `try` statement allows you to define a block of code to be tested for eorrs while it is being executed. The `catch` statement allows you to define a block of code to be executed if an error occurs in the `try` block. You can catch several types of exceptions in a single block.
```java
try {

  //  Block of code to try

} catch (NullPointerException e) {

  //  Code to handle a NullPointerException

} catch (ArithmeticException e) {

  //  Code to handle an ArithmeticException

}
```
