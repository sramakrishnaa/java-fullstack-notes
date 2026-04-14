---
title: Common Mistakes and Best Practices
---

## Common Mistakes

1. **Forgetting break** in switch statements leads to fall-through behavior:
```java
// Bug: will print multiple days
switch (day) {
    case 1:
        System.out.println("Monday");
    case 2:
        System.out.println("Tuesday");  // executes even when day is 1
}
```
2. **Semicolon After if/while/for**
```java
if (x > 10); // Semicolon here!
{
    System.out.println("x is greater than 10");
}
// This block always executes
```

3. **Using assignment instead of comparison:** 
```java
if (x = 5) { }  // Compilation error in Java (good!)
```

4. **Off-by-one errors** in loops:
```java
// Bug: misses last element
for (int i = 0; i < array.length - 1; i++) { }

// Correct
for (int i = 0; i < array.length; i++) { }

```

5. **Modifying loop variables incorrectly:**
```java
// Bug: infinite loop
for (int i = 0; i < 10; i--) { }

int i = 0;
while (i < 10) {
    System.out.println(i);
    // Forgot to increment i
}
```

6. **Wrong Loop Choice**
```java
String[] names = {"Alice", "Bob", "Charlie"};

for (String name : names) {
    // Can't access index here
}
```

7. **Modifying Collection During Enhanced for Loop**
```java
List<String> list = new ArrayList<>(Arrays.asList("A", "B", "C"));

for (String item : list) {
    if (item.equals("B")) {
        list.remove(item); // ConcurrentModificationException
    }
}
```

8. **Floating-Point Comparison**
```java
double a = 0.1 + 0.2;
if (a == 0.3) { // May not work due to precision issues
    System.out.println("Equal");
}
```

9. **Comparing strings** with == instead of equals():
```java
// Wrong
if (str == "hello") { }

// Correct
if (str.equals("hello")) { }
```


---

## Best Practices

1. **Always use braces** for if/else and loops, even for single statements, to prevent bugs during maintenance.
2. **Avoid deep nesting** of `if` statements. Consider refactoring into separate methods or using early returns.
3. **Use meaningful conditions** and avoid magic numbers:
```java
   // Bad
if (status == 1) { }

// Good
final int ACTIVE = 1;
if (status == ACTIVE) { }
```
4. **Choose the right** loop based on your needs. Use `for` when iterations are known, `while` when they depend on conditions, and `for-each` for simple traversal.
5. **Be cautious with infinite loops** and always ensure a proper exit condition.
   




---

## Performance Considerations
The choice between different control structures can impact performance. `for-each` loops are generally as fast as traditional `for` loops. `Switch` statements with many cases can be optimized by the JVM into jump tables, making them faster than equivalent `if-else` chains for certain scenarios.