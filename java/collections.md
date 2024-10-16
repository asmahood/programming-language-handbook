# Collections

## Introduction
Java provides a **Collections Framework** that provides data structures and algorithms. The collections framework provides a hierarchical relationship between its interfaces. All interfaces in the collections framework are generic. Collections are available in the `java.util` package.
```
- Iterable (I)
  - Collection (I)
    - List (I)
      - ArrayList (C)
      - LinkedList (C)
      - Vector (C)
        - Stack (C)
    - Queue (I)
      - PriorityQueue (C)
      - Deque (I)
        - LinkedList (C)
        - ArrayDeque (C)
    - Set (I)
      - HashSet (C)
      - LinkedHashSet (C)
      - SortedSet (I)
        - TreeSet (C)
```

## Collection
Implementing classes may implement `Collection` methods and add restrictions to them like a `Set` does to only contain unique elements. Also, implementing classes or extending interfaces do not need to implement all methods and instead will throw an `UnsupportOperationException` when a `Collection` method is not implemented correctly.

Some methods `Collection` defines are:
- `add`: Adds elements to the collection
- `remove`: Removes elements from the collection
- `addAll`: Takes a `Collection` argument and adds all the elements
- `isEmpty`: Returns `true` if the collection is empty
- `size`: Returns the number of elements in the collection
- `stream`: returns a `Stream` over the elements in the collection
- `toArray`: returns an array with all elements in the collection
```java
Collection<Integer> collection = new ArrayList<>();
collection.add(4);
collection.add(8);

boolean isEmpty = collection.isEmpty(); // false
int collectionSize = collection.size(); // 2

Integer[] collectionArray = collection.toArray(new Integer[0]);
```

### Algorithms
The `Collection` class has many static methods that provide useful algorithms:
- `binarySearch`: preforms a binary search over a `List` to find the specified object and returns the index if found.  This method is overloaded to also accept a `Comparator` to define a custom ordering policy. 
*Note: this method only provides the correct value if the elements in the List are sorted.*
- `max`: Returns the maximum element in the `Collection`. Also overloaded to accept a `Comparator` to define a custom ordering policy.
- `min`: Returns the minimum element in the `Collection`. Also overloaded to accept a `Comparator` to define a custom ordering policy.
- `reverse`: Reverses the order of the elements in a `List`.
- `sort`: Sorts the `List` passed in as an argument. Also overloaded to accept a `Comparator` to define a custom ordering policy.

### Aggregate Operations
A `Stream` is a sequence of elements created from a `Collection` source. A `Stream` can be used as input to a pipeline, which defines a set of aggregate operations (methods that apply transformations to a `Stream` of data). The output of an aggregate operation serves as the input of the next operation (these are known as intermediate operations) until we reach a terminal operation, which is the final operation in a pipeline that produces some non-`Stream` output. 

## List
- Collection where elements are ordered in a sequence
- Allow duplicates
- Allow control of where elements are inserted in the sequence
- Are dynamically sized
- Can be iterated through using enhanced `for` loops.

The collections framework provides many `List` implementations two of which are:
1. `ArrayList` 
2. `LinkedList`
Below is an example of using the `ArrayList` implementation

```java
List<Integer> intList = new ArrayList<>(); // Empty `List`
intList.add(4); // 4
intList.add(6); // 4, 6
intList.add(3); // 4, 6, 3
intList.set(1, 3); // 4, 3, 3

int a = intList.get(2); // a = 3
int b = intList.indexOf(3); // b = 1

List<Integer> subIntList = intList.subList(1,3); // subIntList -> 3, 3
```

## Set
- Collection of unique elements
- Can be iterated through using enhanced `for` loops.

The collections framework provides different implementations of a `Set` that have different use cases

### HashSet
The `HashSet` implementation has the best performance when retrieving or inserting elements but cannot guarantee order. Example of creating a `HashSet`:
```java
Set<Integer> intSet = new HashSet<>();  // Empty set
intSet.add(6);  // true - 6  
intSet.add(0);  //  true - 0, 6 (no guaranteed ordering)
intSet.add(6);  //  false - 0, 6 (no change, no guaranteed ordering)

boolean isNineInSet = intSet.contains(9);  // false
boolean isZeroInSet = intSet.contains(0);  // true
```

### TreeSet
The `TreeSet` implementation does not perform as well on insertion and deletion of elements but does keep elements stored in order based on their values (can be customized).

### LinkedHashSet
The `LinkedHashSet` implementation has slightly slower performance on insertion and deletion of elements than a `HashSet` but keeps elements in insertion order.

## Queue
A `Queue` is First In First Out data structure in which elements are inserted at the tail (back) of the collection and removed from the front. A `Queue` has two types of access methods for inserting, removing, and getting the element at the head of the queue. `Queue`'s can also be iterated through using an enhanced `for` loop.

The following methods throw an exception when:
- `add`: there is no space for the element
- `remove`: there are no elements to remove
- `element`: there are no elements to get

The following methods return a special value:
- `offer`: `false` when there is no space for the element
- `poll`: `null` when there are no elements to remove
- `peek`: `null` when there are no elements to get

The methods that return a special value should be used when working with a statically sized `Queue` and the exception throwing methods when using a dynamic `Queue`.

There are many implementations of a `Queue` including:
- `LinkedList`: useful when a basic `Queue` implementation is needed
- `PriorityQueue`: ensures the top element is the smallest relative to the data's natural ordering (or custom ordering policy provided).

### LinkedList
```java
Queue<String> stringQueue = new LinkedList<>();
stringQueue.add("Mike"); // true - state of queue -> "Mike"
stringQueue.offer("Jeff"); // true - state of queue -> "Mike", "Jeff" 

String a = stringQueue.remove() // Returns "Mike" - state of queue -> 1
String b = stringQueue.poll() // Returns "Jeff" - state of queue -> empty
String c = stringQueue.peek() // Returns null
String d = stringQueue.element() // Throws NoSuchElementException
```

### PriorityQueue
*Note: an enhanced `for` loop makes no guarantee in the ordering of elements after the head.*

## Deque
A `Deque` allows you to access elements from the front and the back of the queue. The `Deque` interface has two types of methods for manipulating the front and the back of the collection.

The following methods throw an exeception:
- `addFirst, addLast`: when there is no space to add an element
- `removeFirst, removeLast`: there is no element to remove
- `getFirst`, `getLast`: there is no element to get

The following methods return a special value:
- `offerFirst, offerLast`: `false` when there is no space to add an element
- `pollFirst, pollLast`: `null` when there is no element to remove
- `peekFirst, peekLast`: `null` when there is no element to get

A `Deque` has many implementations including:
- `LinkedList` - not optimized but more flexible as it can be used as a list, queue, or deque
- `ArrayDeque` - preferred implementation when needing to manipulate elements at the front and back of a collection

If we iterate through a `Deque` using an enhanced `for` loop, the elements would be processed from front to back like a standard `Queue`. However, we can also iterate through a `Deque` from front to back by using an iterator from the `descendingIterator` method and a `while` loop like so:

```java
// Assuming `stringDeque` has elements front -> "Mike", "Jack", "John" <- back

Deque<String> stringDeque = new ArrayDeque<>();
stringDeque.addLast("Mike");
stringDeque.addLast("Jack");
stringDeque.addLast("John");

Iterator<String> iterator = stringDeque.descendingIterator();

while(iterator.hasNext()) {
  System.out.println(iterator.next());
}
// OUTPUT TERMINAL:  "John", "Jack", "Mike"
```

### ArrayDeque
```java
Deque<String> stringDeque = new ArrayDeque<>();
stringDeque.addFirst("A"); // Front -> "A" <- end
stringDeque.offerFirst("B"); // Return `true` - front -> "B", "A" <- end
stringDeque.offerLast("Z"); // Returns `true` - front -> "B", "A", "Z" <- end

String a = stringDeque.removeFirst()  // Returns "B" - front -> "A", "Z"
String b = stringDeque.pollLast()  // Returns "Z" - front -> "A" <- back
String c = stringDeque.removeLast()  // Returns "A" - empty deque

String d = stringDeque.peekFirst()  // Returns null
String e = stringDeque.getLast() // Throws NoSuchElementException
```

## Map
`Map` is another interface in the collections framework that doesn't fit into the hierarchy. `Map` defines generic interface for an object that holds key-value pairs as elements. The key is used to retrieve some value. A key must be unique and map to exactly one value. There are many implementations of `Map`, but this document will focus on the `HashMap` implementation.

A map has the following methods for accessing elements:
- `put`: Sets the value that a key maps to. Note that this method replaces the value a key mapped to if the key was already present in the `Map`.
- `get`: Gets, but does not remove, the value the provided key argument points to if it exists. This method returns `null` if the key is not in the `Map`.

A `Map` can be iterated over with an enhanced `for` loop:
```java
// Given a map, `myMap`, with the following key-value pairs { "Hello" -> "World" }, { "Name" -> "John"}
for (String s: myMap.keySet()){
  System.out.println("key: "+s+", value: "+myMap.get(s));
}
// OUTPUT TERMINAL:
// key: Name, value: John
// key: Hello, value: World
```

### HashMap
- Defines no specific ordering for the keys
- Most optimized implementation for retrieving values
- Implementation of a hash table

```java
Map<String, String> myMap = new HashMap<>();

myMap.put("Hello", "World") // { "Hello" -> "World" }
myMap.put("Name", "John") //   { "Hello" -> "World" }, { "Name" -> "John" }

String result = myMap.get("Hello") // returns "World" 
String noResult = myMap.get("Jack") // return `null`
```
