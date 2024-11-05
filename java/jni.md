# JNI
JNI stands for Java Native Interface. JNI is a powerful tool utilized especially to implement a coding language such as C++ that can overcome constraints in a Java program. For example, the Java language supports automatic memory allocation, but a programmer may encounter a situation in which they may choose to write a portion of their code in C++ so that they can control memory allocation for performance optimization of their program. In such a case, implementing a JNI would be helpful to the programmer because, unlike Java, native languages like C and C++ allow programmers to manipulate and manage memory allocation.

JNI is implemented on Java virtual machines (JVM). JVM is the platform on which Java code is loaded and executed. In order to run Java code with JNI, it is crucial that the Java program with JNI is correctly compiled and linked. JNI includes its own commands to assist in doing so.

## Implementing JNI into Java
When creating a mehtod that is meant to be used by JNI, you will need to use the keyword `native` when declaring the method:

```java
private native void totalSum();
```
Arguments and return values can be defined as any other method:
```java
public int void totalSum(double num1, double num2);
```

*Note: there is no implementation of `totalSum`. This is because the implementation of the method will be written in the native language that is being used on the other end of the JNI.*

An important element needed in the Java code is the `System.loadLibrary()` method. This is used on the Java side, usually in the main method to load the dynamic library that holds the native code. To implement a native method in native code, compile the Java program and generate a `.h` file:
```java
javac -h . FindSum.java
```
