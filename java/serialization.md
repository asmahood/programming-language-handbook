# Serialization

Often when creating Java applications and working with objects, we find the need to persist them. Specifically, we need to be able to store an object’s state (member fields) in files, in memory, or in a database. Java provides the `Serializable` interface to do just that.

## Implementing Serialization

For example:
```java
public class Person implements Serializable {
  private String name;
  private int age;
} 
```
By implementing `Serializable`, the JVM will know how and what to do when a `Person` object needs to be serialized. We don't need to override a method and implement it to be able to serialize a `Person` object. This is because `Serializable` is a **marker** interface. A marker interface provides runtime information to the JVM about the class and does not have any methods associated with it. The JVM defines a default way for classes that implement `Serializable` to have their objects serialized. The interface provides run-time information about the object field’s type and value for serialization and it takes care of converting it into a stream of bytes. 

Although there are no methods that need to be implemented, it is important for the implementing class to provide a `serialVersionUID`:
```java
public class Person implements Serializable {
  private String name;
  private int age;
  private static final long serialVersionUID = 1L; 
} 
```
This member acts as an identifier for the JVM to choose the proper class to convert to a stream of bytes back into an object. There are multiple ways to get a `serialVersionUID`:
- You can have the JVM define one for you. This is not ideal because, depending on the JVM you have, you’ll get a different value and this may cause deserialization to fail.
- You can have your IDE generate one for you. This is better than the first option but you’ll need to ensure that your IDE has this feature.
- You can define the `serialVersionUID` explicitly in the class. This is the preferred option because you don’t need to rely on the JVM or your IDE to ensure proper deserialization.

## Serializing Objects to a File
To serialize objects to a file, you will need two helper classes:
- `FileOutputStream` - used to help write to files
- `ObjectOutputStream` - used to write a serializable object to an output stream

For example:
```java
public class Person implements Serializable {
  private String name;
  private int age;
  private static final long serialVersionUID = 1L; 

  public Person(String name, int age) {
    this.name = name;
    this.age = age;
  }  

  public static void main(String[] args) throws FileNotFoundException, IOException{
    Person michael = new Person("Michael", 26);
    Person peter = new Person("Peter", 37);
        
    FileOutputStream fileOutputStream = new FileOutputStream("persons.txt");
    ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);
        
    objectOutputStream.writeObject(michael);
    objectOutputStream.writeObject(peter); 
  }
}
```
In this example:
- Added a constructor to the Person class we defined in the previous lesson.
- Defined main() and initialized two Person objects - michael and peter.
- Initialized a FileOutputStream object in main() which will create and write a stream of bytes to a file named persons.txt.
- Initialized an ObjectOutputStream object in main() which will help serialize an object to a specified output stream.
- Used objectOutputStream.writeObject() in main() to serialize the michael and peter objects to a file.

After execution, the file `persons.txt` will contain a stream of bytes corresponding to the type and value of the information in the fields of the objects `michael` and `peter`. 

## Deserializing an Object to a File
To deserialize objects, we will again use helper classes:
- `FileInputStream` - used to read a file
- `ObjectOutputStream` - used to read a serialized stream of bytes
```java
public class Person implements Serializable {
  public static void main(String[] args) throws FileNotFoundException, IOException, ClassNotFoundException {

    FileInputStream fileInputStream = new FileInputStream("persons.txt");
    ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);
        
    Person michaelCopy = (Person) objectInputStream.readObject();
    Person peterCopy = (Person) objectInputStream.readObject();
  }
}
```

In the example above we:
- Initialized `FileInputStream` and `ObjectInputStream` in `main()` which will read a file and transform a stream of bytes into a Java object.
- Created a `Person` object named `michaelCopy` by using `objectInputStream.readObject()` to read a serialized object.
- Created a `Person` object named `peterCopy` by using `objectInputStream.readObject()` to read a serialized object.

Note that the deserialized objects will be in the order that they were serialized in and we need to explicitly typecast the `readObject()` return value back into the type of object we serialized. 

The JVM ensures it deserializes the object using the correct class file by comparing the `serialVersionUID` in the class file with the one in the serialized object. If a match is not found an `InvalidClassException` is thrown. Also, `readObject()` throws a `ClassNotFoundException` when the class of the serialized object cannot be found.

## Serializable Fields
By default, the JVM ignores static fields and includes all fields (even those marked as `final` and `private`) when serializing objects.

You can instruct the JVM to ignore non-static fields using the `transient` keyword. A field marked as `transient` will have its valued ignored during serialization and instead receive the default value for that type of field.
```java
public class Person implements Serializable {
  private String name;
  private int age;
  private static int numberOfPeople = 10;
  private transient int yearBorn;  
} 
```
Note that a constructor is not called during deserialization for the deserialized type object. Object fields are set using **reflection**. A constructor is only called for the first non-serializable class in the parent hierarchy of the deserialized object.

### Serializing Associated Fields
For a reference types to be serializable, they must also implment the `Serializable` interface. If the reference type did not implement Serializable, then we would get a `NotSerializableException` thrown.

## Custom Serialization
We can customize serialization by implementing methods `readObject` and `writeObject` in our class.
```java
public class DateOfBirth {
  private int month;
  private int day;
  private int year;

  // constructors and getters
}

public class Person implements Serializable {
  private String name;
  private DateOfBirth dateOfBirth;

  private void writeObject(java.io.ObjectOutputStream stream) throws IOException{
    stream.writeObject(this.name);
    stream.writeInt(this.dateOfBirth.getMonth());
    stream.writeInt(this.dateOfBirth.getDay());
    stream.writeInt(this.dateOfBirth.getYear());
  }

  private void readObject(java.io.ObjectInputStream stream) throws IOException, ClassNotFoundException{
    this.name = (String) stream.readObject();
    int month = (int) stream.readInt();
    int day = (int) stream.readInt();
    int year = (int) stream.readInt();
    this.dateOfBirth = new DateOfBirth(month, day, year);
  } 
}
```

In the example above:
- We have two classes: `Person` which implements `Serializable` and `DateOfBirth` which does not.
- `Person` has a reference field of type `DateOfBirth`.
- If we were to use the default serialization process, we would get a `NotSerializableException` because `DateOfBirth` does not implement `Serializable`.
- We implement `writeObject()`, which must throw `IOException`, to serialize a `DateOfBirth` object by manually serializing all of its fields separately. We also serialize the serializable `String` field.
- We implement `readObject()`, which must throw `IOException` and `ClassNotFoundException`, to deserialize a `Person` object by reading the `int` fields that are a part of `DateOfBirth` and creating a new `DateOfBirth` object with the provided constructor. This new object is used to set the `dateOfBirth` field in `Person`.

