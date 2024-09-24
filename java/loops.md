# Loops

## While Loop
A while loop is constructed like so
```java
while (condition) {
    // ...
}
```

## For Loop
A `for` loop is made up of three parts:

1. An initialization of an iterator variable
2. A boolean condition
3. An increment/decrement statement

```java
for (int i = 0; i < 3; i++) {
    // ...
}
```

The initialization is only run once at the start. Then the condition is checked. If the condition evaluates to `true`, the body of the loop is run. Once the body is finished, the increment/decrement operation is evaluated. Then the process is repeated starting at evaluating the condition.

## For-Each Loop
For-Each loops allow you to directly loop through each item in a list (like an array or `ArrayList`). The syntax for a for-each loop includes:

1. A loop variable, with the same datatype as the values stored in the list
2. A `:` followed by the list

```java
for (String inventoryItem : inventoryItems) {
  // Print element value
  System.out.println(inventoryItem);

}
```

Note that if you try to assign a new value to the loop variable, the value in the array will not be changed. This is because the loop variable is assigned a copy of the item in the list.

## Break
If you want to exit the loop before it finishes, uses the `break` keyword. Similar functionality if using `return`.

## Continue
If you want to skip an iteration and move onto the next, use the `continue` keyword.

## Removing an Element While Traversing
When an element is removed from an `ArrayList`, all other elements after will have their index shifted by `-1`. If using a counter variable, do not increase the counter after deleting an element. If using a `for` loop, once you remove an item, decrement the loop control variable. **Note: Avoid manipulating the size of an ArrayList when using an enhanced `for` loop. Adding or removing elements can cause a `ConcurrentModifcationException`**.
