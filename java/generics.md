# Generics

## Generic Classes
To create a generic class:
```java
public class Box <T> {
  private T data;

  public Box(T data) {
    this.data = data; 
  }

  public T getData() {
    return this.data;
  }  
}
```
- The type parameter must be specified within the diamond operator (`<>`) after the class name.
- The type parameter, `T`, is similar to a method parameter but instead receives a class or interface type as an argument as opposed to a reference or primitive type.
- The constructor accepts a `T`-type parameter to initialize data.
- The getter method returns the type parameter `T` when returning data

To create a new instance of a generic class:
```java
Box<String> myStringBox = new Box<>("Apple");
```
- Needing the diamond operator with the class or interface type argument, `<String>` in this example, after the class name.
- Needing the empty diamond operator before calling the constructor `new Box<>("Apple")`.

*Note: It is best practice to keep type parameters to single uppercase letters. Some conventions are:*
- `E` - Elements
- `K` - Key
- `N` - Number
- `T` - Type
- `V` - Value
- `S` (or `U` or `V`) - for multiple type parameters

*Note: Before Java 7, generics had to be created like `Box<String> myStringBox = new Box<String>("Apple");`. This is no longer necessary in newer Java versions because of Java's type inference*

### Using Primitive Types in Type Parameters
You cannot use primitive types in type parameters (ex: `int`, `double`, `float`). To use primitive types, you need to specify the [wrapper class](variables.md#primitive-data-types) of the primitive data type.
```java
Box<Integer> intBox = new Box<>(56);
```
*Note: we are able to pass `56` as the argument to the constructor because of **autoboxing**. Autoboxing allows wrapper classes to take primitive values and convert them to their corresponding wrapper object by automatically calling the `valueOf` method. For example, the following statements are equivalent:*
```java
Integer a = 56;  // Autoboxing, automatic call to `valueOf()`
Box<Integer> intBox1 = new Box<>(a);
Box<Integer> intBox2 = new Box<>(56);  // Autoboxing, automatic call to `valueOf()`
Box<Integer> intBox3 = new Box<>(Integer.valueOf(56));

// Return back to primitive (unboxing)
Integer a = 56;
int aPrimitive1 = a.intValue();  // Return primitive `int` value from `Integer` object
int aPrimitive2 = a;  // Unboxing, automatic call to `intValue()`
```

## Generic Interfaces
You can create a generic interface like so:
```java
public interface Replacer<T> {
  void replace(T data);
}
```
A generic interface can be implemented by a generic class and its generic type parameter can be used as the argument to the interface type parameter. For example:
```java
public class Box <T> implements Replacer<T> {
  private T data;
  
  @Override
  void replace(T data) {
    this.data = data; 
  }
}
```
A non-generic class can also implement a generic interface like so:
```java
public class StringBag implements Replacer<String> {
  private String data;
  
  @Override
  void replace(String data) {
    this.data = data; 
  }
}
```
Notice that the `replace()` parameter data has a `String` type as opposed to the generic `T` in the previous example. 

To create `interface` type references:
```java
Replacer<Integer> boxReplacer = new Box<>();  // Using generic `Box` implementation
Replacer<String> bagReplacer = new StringBag();  // Using non-generic `StringBag` implementation
```

## Generic Methods

You can create a generic method as so:
```java
public class StringBox {
  private String data;

  public <T> boolean isString(T item) {
    return item instanceof String; 
  }
}

StringBox box = new StringBox();
box.isString(5); // Returns false
```
This can also be done with static methods:
```java
public class StringBox {
  private String data;

  public static <T> boolean isString(T item) {
    return item instanceof String; 
  }
}
StringBox.isString(5);  // Returns false
```
