# Classes

## Defining a class
To define a class:
```java
public class Car {
  // ...
}
```

## Defining Access
Defining access means defining what parts of a class other classes can access/call. You can define access on:
- Instance variables
- Methods
- Constructors
- Classes themselves

### Public
If you declare something as `public`, this means any class can access/call this part of the code. To declare something as public, place the `public` keyword at the start of the declaration/definition/function signature.

### Private
When a instance variable or method is marked as `private`, then these variables/methods can only be accessed/called within the same class.i

## Defining a Constructor
A constructor is a special method defined within the class used to initialize the fields when creating an instance. The constructor must be the same name as class itself. Generally, constructors are defined as `public`.

```java
public class Car {
    public Car() {
        // ...
    }
}
```

A class can have multiple constructors, and they are differentiated based on their parameters. For example
```java
public class Car {
    public String color;
    public int mpg;
    public boolean isElectric;

    public Car(String carColor, int milesPerGallon) {
        color = carColor;
        mpg = milesPerGallon;
    }

    public Car(boolean electricCar, int milesPerGallon) {
        isElectric = electricCar;
        mpg = milesPerGallon;
    }
}
```

When no constructors are defined, the Java compiler creates a default constructor that assigns default values to an instance. Default values can be created by assigning values to the instance fields. For example:
```java
public class Car {
    public String color = "red";

    public main(String[] args) {
        Car ferrari = new Car(); // #=> ferrari.color == "red"
    }
}
```

### Constructor Parameters
To include parameters in a constructor, you can add them like so:
```java
public class Car {
    public String color;

    // Constructor with one parameter: 'carColor'
    public Car(String carColor) {
        color = carColor; // Assign the instance field color to the value of carColor
    }
}
```

## Creating an instance of a class
Using the assignment operator (`=`), you can create a new instance of an object using `new`.
```java
Car ferrari = new Car();
```
Note that the `ferrari` variable is now a referencedata type rather than a primitive. Thus we can use `null` to initialize a reference datatype, therefore it would have a void reference. It’s important to understand that using a null reference to call a method or access an instance variable will result in a NullPointerException error.

## Adding fields to a class
Fields are characterized by their "has-a" relationship with an object. For example, a car "has-a" color. You can declare fields inside the class outside any methods. Then, these fields will be available in the scope of any method.
```java
public class Car {
    public String color;
    public int year;
    public String modelName;
    public String make;

    public Car() {}
}
```

### Assigning values to instance fields
Fields can be set in three ways:
- If a field is `public`, they can be set like `instanceName.fieldName = someValue;`
- They can be set in class methods
- They can be set in the constructor

## Methods
A method is characterized by its **signature** (name, number of, and parameters of the method). There are two types of parameters: **formal parameters**, and **actual parameters**.
- Formal parameters: variables that will store data that is passed into a method. It specifies the type and name of the data.
- Actual parameters:

When passing arguments, a copy of the argument value is passed to the parameter rather than the actual variables. This is called **call by value**.

### Defining methods

To define a method, you need three things:
1. The visibility (`public`, `private`, etc.)
2. The return type (`void`, `int`, etc.)
3. The name of the method

```java
public void checkBalance() {}
```

### Calling methods
Non-static methods are available to be called on instances of the class.

### Adding parameters
Similar to constructors, parameters are added by including the datatype followed by the parameter name in the method declaration.

#### Method Overloading
Method overloading is possible in Java by creating two methods with the same name, however the method signatures must be different.

### Returning values from methods
You can return a value from a method using the `return` keyword. THis will exit the execution of the method. The value returned must match the return type designated by the methods return type. When returning a primitive datatype, a copy of the value will get returned, which is known as **return by value**. When an object is returned, a **reference** to the object is returned instead of a copy of it.

### Accessor and Mutator Methods
To support encapsulation, we often make our instance variables private. To let other classes access a private instance variable, we write **accessor** methods (also known as getters).
```java
public class Dog {
  private String name;
    
  //Other methods and constructors

  public String getName() {
    return name;
  }
}
```
Private instance variables often have **mutator** methods (also known as setters) which allow other classes to change the stored value in a private instance variable. These methods are often marked as `void` and only have one parameter.

```java
public class Dog {
    private String name;

    pubic void setName(String newName) {
        name = newName;
    }
}
```

## The `This` Keyword
The `this` keyword is a reference to the current object. It can be used to get the current objects instance variable, call methods, or passed as a parameter. It is particularly useful when parameters of a method have the same name as an instance variable, so you can use the `this` keyword to specify the instance variable. By default, Java will use the parameter. It is also useful for being more clear about what the thing you are refering to comes from.
```java
public class Computer {
  public int brightness;
  public int volume;
  
  public void setBrightness(int inputBrightness){
    this.brightness = inputBrightness;
  }

  public void setVolume(int inputVolume){
    this.volume = inputVolume;
  }

  public void resetSettings(){
    this.setBrightness(0);
    this.setVolume(0);
  }

  public void pairWithOtherComputer(Computer other){
      // Code for method that uses the parameter other
  }

  public void setUpConnection(){
    // We use "this" to call the method and also pass "this" to the method so it can be used in that method
    this.pairWithOtherComputer(this);
  }
}
```

## Static Methods and Variables
Static methods and variables belong to an entire class, not a specific instance. They can be accessed/called using the class name and the `.` operator. To declare a variable/method as static, add the `static` keyword after the accessiblity keyword.
```java
public class Dog{

  // Static variables
  public static String genus = "Canis";

  //Instance variables
  public int age;
  public String name;

  public Dog(int inputAge, String inputName){
    this.age = inputAge;
    this.name = inputName;
  }

  public static String getGenus() {
    return Dog.genus;
  }
}
```
One important note is that static methods cannot interact with non-staic instance variables.

## Printing Objects
If you were to print an object, you would get something like `Car@6bc7c054`, which is the address of the location in memory where the object is stored. If we wanted to print something more descriptive, we can add a `toString()` method to our class which returns a `String`. This will be printed instead. For example:
```java
class Car {
    String color;

    public Car(String carColor) {
        color = carColor;
    }

    public static void main(String[] args){
        Car myCar = new Car("red");
        System.out.println(myCar);
    }

   public String toString(){
       return "This is a " + color + " car!";
   }
}
```

