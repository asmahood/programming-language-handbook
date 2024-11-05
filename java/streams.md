# Streams
Streams were introduced in Java 8. In a stream, intermediate operations are lazily executed and return results in the form of additional streams, which allow for the pipelining of those results. Terminal operations mark the end of the stream and return the final result.

## Sequential Streams

### Intermediate Operations

#### Map
`map` returns a stream consisting of the results after applying a given function to the elements of this stream:
```java
List numbers = Arrays.asList(1,2,3,4);
List square = numbers.stream().map(x->x*x).collect(Collectors.toList());
```

#### Filter
`filter` selects elements per a predicate passed as an argument:
```java
List names = Arrays.asList(“Alpha”,”Beta”,”Omega”);
List find = names.stream().filter(s->s.startsWith(“O”)).collect(Collectors.toList());
```

#### Sorted
`sorted` sorts the stream:
```java
List names = Arrays.asList(“Omega”,”Alpha”,”Beta”);
List sorted = names.stream().sorted().collect(Collectors.toList());
```

### Terminal Operations

#### Collect
`collect` returns the result of the intermediate operations performed on the stream:
```java
List numbers = Arrays.asList(1,2,3,4,2);
Set squareSet = numbers.stream().map(x->x*x).collect(Collectors.toSet());
```

#### For Each
`forEach` iterates through every element of the stream:
```java
List numbers = Arrays.asList(1,2,3,4);
numbers.stream().map(x->x*x).forEach(y->System.out.println(y));
```

#### Reduce
`reduce` reduces the elements of a stream to a single value (this takes a `BinaryOperator` as a parameter):
```java
List numbers = Arrays.asList(1,2,3,4);
int even = numbers.stream().filter(x->x%2==0).reduce(0,(ans,i)->ans+i);
```

## Parallel Streams
Streams are good for parallel processing because they do not alter the original object. Java Parallel Streams divide a running process into multiple streams that execute in parallel on separate cores, returing a combined result of all the individual outcomes. However, the order of execution is not under control so only use parallel streams when the order of execution doesn't matter.

To create a parallel stream, call the `parallelStream` method on a `Collection` of some type:
```java
File file = new File(filePath);
List<String> textLines = Files.readAllLines(file.toPath());
textLines.parallelStream().forEach(System.out::println);
```
Alternatively, call the `parallel` method on a `BaseStream` object:
```java
File file = new File(filePath);
Stream<String> textLines = Files.lines(file.toPath());
textLines.parallel().forEach(System.out::println);
textLines.close();
```
