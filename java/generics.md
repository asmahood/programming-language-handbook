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

## Type Upper Bounds
If you want to restrict what classes or interfaces could be used as a type argument. To do this, use the `extends` keyword in the type parameter:
```java
public class Box <T extends Number> {
  private T data;
}
```
This examples means that `T` can be a `Number` or any of its subclasses (or interfaces). I.e.
```java
Box<Integer> intBox = new Box<>(2);  // Valid type argument
Box<Double> doubleBox = new Box<>(2.5);  // Valid type argument
Box<String> stringBox = new Box<>("hello");  // Error
```

### Specifying Multiple Bounds
Java allows you to specify multiple bounds for a type parameter using the `&` operator:
```java
public class Box <T extends Number & Comparable<T>> {
  private T data; 
}
```
*Note: When specifying multiple bounds any upper bound that is a class must come first followed by any interfaces.*

## Wildcards
When you don't need the strict type checking of using type parameters, you can use **wildcards** (denoted by `?`). This represents an unknown type when used in generic methods.
```java
public class Util {
  public static void printBag(Bag<?> bag) {
    System.out.println(bag.toString()); 
  }
}
Bag<String> myBag1 = new Bag("Hello");
Bag<Integer> myBag2 = new Bag(23);
Util.printBag(myBag1);  // Hello
Util.printBag(myBag2);  // 23
```
This syntax is equivalent to:
```java
public static <T> void printBag(Bag<T> bag) {
  System.out.println(bag.toString()); 
}
```
In general, type parameters should be used when there is a relationship between the type of arguments and the return type.

Upper and lower bounds can also be used with wildcards.

### Lower Bounds
A lower bound restricts a wildcard to a class or interface and any of its parent types:
```java
public class Util {
  public static void getBag(Bag<? super Integer> bag) {
    return bag;
  }
}
```
In the example above:
- Used the `super` keyword to restrict the argument to `getBag` to be a `Bag` of `Integer`, `Number`, or `Object`.
- If a call to `getBag` with `Bag<Double>` is made, it would result in an error
  - This is because double is not an `Integer` or one of its parents.

*Notes:*
- *Lower bounds cannot be used with generic type parameters, only wildcards*
- *A wildcard cannot have a lower bound **AND** an upperbound (best to use type parameter in this case)*

### General Guidelines for Wildcards
- An upper bound wildcard should be used when the variable is being used to serve some type of data to our code
- A lower bound wildcard should be used when the variable is receiving data and holding it for later use.
- When a variable that serves data is used and only uses `Object` methods, an unbounded wildcard is preferred.
- When a variable needs to serve data and store data for later use, a wildcard should not be used (use a type parameter instead).
