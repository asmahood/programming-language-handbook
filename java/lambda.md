# Lambdas
Lambdas can define the method with its parameter(s) and its return value in a small block of code. For example:
```java
List<Integer> evenList = intList.stream()
  .filter((number) -> {return number % 2 == 0;})
  .map(evenNum -> evenNum*2)
  .collect(Collectors.toList());
```
The lambda defines all the parameters before the arrow (`->`) symbol and defines the function’s body after. You can omit the parameter parentheses `()` when there is only one parameter and omit the curly braces `{}` and return when the lambda body is one line.
