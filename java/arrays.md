# Arrays

# Introduction
In Java, arrays are zero indexed.

## Creating an Array

### Explictly
To declare an array, provide the datatype followed by `[]`. For example
```java
double[] prices; // Creates an array of doubles
```
You can also declare and initialize on the same line using an initializer list.
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

# ArrayLists
Arrays are limited by the fact that once they are created, it has a fixed size. To create mutable and dynamic lists, we can use the `ArrayList` class which allows us to
- Store object references as elements
- Store elements of the same type
- Access elements by index
- Add elements
- Remove elements

## Importing ArrayLists
To use ArrayLists, we have to import it
```java
import java.util.ArrayList
```

## Creating an ArrayList
To create an `ArrayList`, you need to declare what type of objects the it holds inside `<>`. Since `ArrayList` uses generics (which define classes and objects as parameters), primitive types cannot be used in an ArrayList. To use primitives in an `ArrayList`, you need to specify the type like `Integer`, `Double`, or `Character` as an example.

To initialize an empty `ArrayList` we can use the `new` keyword
```java
// Declaring
ArrayList<Integer> ages;

// Initializing
ages = new ArrayList<Integer>();

// Declaring and Initializing (Defining)
ArrayList<String> babyNames = new ArrayList<String>();
```

### Creating an ArrayList of Different Elements
You can create an `ArrayList` that holds different datatypes. To do this, when defining an `ArrayList`, leave the template parameter empty. This will allow the `ArrayList` to hold any values inside it. Technically, all the values in this list are considered `Object`'s, so they will not have access to some of their methods without type casting.

## Adding Items
The `ArrayList` class comes with an `add()` method which inserts elements into the array. This method can be used into two ways:

1. If only one argument is supplied, `add()` will add the supplied item to the end of the list
```java
ArrayList<Car> carShow = new ArrayList<Car>();

carShow.add(ferrari);
// carShow now holds [ferrari]
carShow.add(thunderbird);
// carShow now holds [ferrari, thunderbird]
carShow.add(volkswagen);
// carShow now holds [ferrari, thunderbird, volkswagen]
```

2. If you want to add an item to a specific position, you can supply the index of where the item should go and the item
```java
// Insert object corvette at index 1
carShow.add(1, corvette);
// carShow now holds [ferrari, corvette, thunderbird, volkswagen]
```

## Getting the length of the list
To get the number of elements in an `ArrayList`, you can call the `size()` method.
```java
carShow.size() // #=> 4
```

## Accessing the List

### By Index
To access a specific item by index in an `ArrayList`, we cannot use the `[]` operator. Instead we use the `get()` method.
```java
ArrayList<String> shoppingCart = new ArrayList<String>();

shoppingCart.add("Trench Coat");
shoppingCart.add("Tweed Houndstooth Hat");
shoppingCart.add("Magnifying Glass");

System.out.println(shoppingCart.get(2)); // #=> Prints "Magnifying Glass"
```

### By Value
If you want to find the index of an item in the list you can use the `indexOf()` method with the value of the item you want to find.
```java
shoppingCart.indexOf("Tweed Houndstooth Hat") // #=> 1
```

## Changing an Item in the list
Again, we cannot use the `[]` operator to access and change an element in the `ArrayList`. Instead we have to use the `set()` method. This method takes an index and the new value you want to place at that index.
```java
ArrayList<String> shoppingCart = new ArrayList<String>();

shoppingCart.add("Trench Coat");
shoppingCart.add("Tweed Houndstooth Hat");
shoppingCart.add("Magnifying Glass");

shoppingCart.set(0, "Tweed Cape");

// shoppingCart now holds ["Tweed Cape", "Tweed Houndstooth Hat", "Magnifying Glass"]
```

## Removing an Item
To remove an item from an `ArrayList`, we can use the `remove()` method which takes an index of the item to remove or the value we want to remove.
```java
ArrayList<String> shoppingCart = new ArrayList<String>();

shoppingCart.add("Trench Coat");
shoppingCart.add("Tweed Houndstooth Hat");
shoppingCart.add("Magnifying Glass");

shoppingCart.set(0, "Tweed Cape");

// shoppingCart now holds ["Tweed Cape", "Tweed Houndstooth Hat", "Magnifying Glass"]

// ===== OR =====

ArrayList<String> shoppingCart = new ArrayList<String>();

shoppingCart.add("Trench Coat");
shoppingCart.add("Tweed Houndstooth Hat");
shoppingCart.add("Magnifying Glass");

shoppingCart.remove("Trench Coat");
// shoppingCart now holds ["Tweed Houndstooth Hat", "Magnifying Glass"]
```
If specifying a value, the method will remove the **first** instance of the value.
