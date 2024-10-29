# Regular Expressions
To use regex in Java, we need to import the regex package:
```java
import java.util.regex;
```

## The Pattern Class
The `Pattern` class is used to define a regex pattern we want to find in a string. You can create a pattern like so:
```java
Pattern pattern = Pattern.compile("Codecademy");
Pattern pattern = Pattern.compile("codecademy", Pattern.CASE_INSENSITIVE);
```
The second parameter is used to specify flags:
- `Pattern.CASE_INSENSITIVE` - THe case of letters will be ignored when performing a search.
- `Pattern.LITERAL` - Special characters in the pattern will not have any special meaning and will be treated as ordinary characters when performing a search.
- `Pattern.UNICODE_CASE` - Use it together with the `CASE_INSENSITIVE` flag to also ignore the case of letters outside of the English alphabet.

To match a string against a Pattern, we need to use the `Matcher` class.

## The Matcher Class
The `Matcher` class takes a regular expression defined by a `Pattern` class and performs a search based on the compiled pattern. To create a `Matcher` class:
```java
Pattern pattern = Pattern.compile("Codecademy");

Matcher matcher = pattern.matcher("Welcome to Codecademy!");
```

### Find
The `find` method searches the string for the next match based on the pattern and returns `true` if it finds an occurrence of it. Internally, the `find` method retains a pointer to indicate where it should start searching in the text. The pointer initially starts at the beginning of the text and stops at the next character after matching. If `Matcher` is not reset, the next time `find` is called it will start searching where it left off.

### Matches
The `matches` method returns `true` if the string matches exactly the pattern with no other characters in the string.
