# Arrays

# Introduction
In Java, arrays are zero indexed.

## Creating an Array

### Explictly
To declare an array, provide the datatype followed by `[]`. For example
```java
double[] prices; // Creates an array of doubles
```
You can also declare and initialize on the same line as so
```java
double[] prices = {13.15, 15.87, 14.22, 16.66};
```

### Empty Arrays
To create an empty array, we can do the following
```java
String[] menuItems = new String[5];
```
Empty arrays have to be initialized with a fixed size. Once the size is declared, it cannot be changed.

After declaring the array, we can fill it with values by using `arr[idx] = value`. This can also be used to change the value of an item in a certain position.

When using `new` to create an empty array, each element in the array is initialized with the empty value of its type. Since `String` is a reference type, an array will be filled with `null`s. 

## Importing the Arrays Package
By default, printing an array will return its memory address. If we want a more descriptive printout of the array itself, we need to import a `toString()` method provided by the `Arrays` package. To import this package, at the top of the file write
```java
import java.util.Arrays;
```
To print the contents of the array, use the `Arrays.toString(arr)` static method.i

## Getting an Element by Index
To get a value out of an array using an index, use `arr[idx]`. For example:
```java
double[] prices = {13.1, 15.87, 14.22, 16.66};

System.out.println(prices[1]); // #=> 15.87
```
Accessing an element outside the arrays size will receive an `ArrayIndexOutOfBoundsException`.

## Getting the length of an array
If you need to get the length of an array, you can access the `length` field:
```java
System.out.println(menuItems.length);
```
