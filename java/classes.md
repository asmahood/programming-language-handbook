# Classes

## Defining a class
To define a class:
```java
public class Car {
  // ...
}
```

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

When passing arguments, a copy of the argument value is passed to the parameter rather than the actual variables. This is called **call-by-value**.

### Defining methods

