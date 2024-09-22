# Control Flow

## If-Then Statement
To write an if statement, you can do the following
```java
if (flip == 1) {
    System.out.println("Heads!")
}
```
The contents inside `()` must either reference a boolean variable or be an expression that evaluates to a boolean. If the condition is brief, the curly braces can be omitted.

## If-Then-Else Statement
If you want to write an if-else statment, you can do the following
```java
if (hasPrereq) {
    // Code if hasPrereq == true
} else {
    // Code if hasPrereq == false
}
```

## If-Then-Else-If Statement
To write an if-else-if statement, you can do the following
```java
String course = "Theatre";

if (course.equals("Biology")) {

  // Enroll in Biology course

} else if (course.equals("Algebra")) {

  // Enroll in Algebra course

} else if (course.equals("Theatre")) {

  // Enroll in Theatre course

} else {

  System.out.println("Course not found!");

}
```

## Switch Statement
A switch statment is written like so:
```java
String course = "History";

switch (course) {
  case "Algebra":
    // Enroll in Algebra
    break;
  case "Biology":
    // Enroll in Biology
    break;
  case "History":
    // Enroll in History
    break;
  case "Theatre":
    // Enroll in Theatre
    break;
  default
    System.out.println("Course not found");
}
```
This examples matches the value of the course variable with the value next to the `case` keyword. If they are equal, then the code after the case label runs. The `break` statement exits the switch statement and continues running any code below it. If no value matches, the `default` case is run. If the `break` keyword is not included, the remaining case labels will also be checked.


