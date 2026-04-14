---
title: Introduction
---

# The Primitive Types

Java defines **eight primitive types**. These are the fundamental building blocks for all data in Java.

## Why Primitives Aren't Objects

Java is object-oriented, but primitive types are **not** objects. This might seem contradictory, but there's a good reason: **performance**.

Making these basic types into objects would add overhead to every simple operation. Imagine if adding two numbers required creating objects - programs would be much slower. So Java keeps primitives simple and efficient.


## The Four Categories

The eight primitive types fall into four groups:

1. [Integers](integer-types.md) - Whole numbers (byte, short, int, long)
2. [Floating-point](floating-point-types.md) - Numbers with decimals (float, double)
3. [Characters](character-types.md) - Text symbols (char)
4. [Boolean](boolean-type.md) - True/false values (boolean)


## Primitive Type Hierarchy
``` mermaid
graph TD
    A[Java Primitive Types]

    A --> B[Integers]
    B --> B1[byte]
    B --> B2[short]
    B --> B3[int]
    B --> B4[long]

    A --> C[Floating Point]
    C --> C1[float]
    C --> C2[double]

    A --> D[Character]
    D --> D1[char]

    A --> E[Boolean]
    E --> E1[boolean]
```


## Key Characteristics
 
| Type | Size | Purpose | Example |
|------|------|---------|---------|
| [byte](/java-fullstack-notes/Java/data-types-and-variables/primitive-types/integer-types.html#byte-the-smallest-integer) | 8 bits | Small integers, binary data | `byte age = 25;` |
| short | 16 bits | Medium integers (rarely used) | `short year = 2024;` |
| int | 32 bits | Standard integers | `int count = 1000;` |
| long | 64 bits | Large integers | `long distance = 9876543210L;` |
| float | 32 bits | Decimal numbers (less precise) | `float price = 19.99f;` |
| double | 64 bits | Decimal numbers (more precise) | `double pi = 3.14159;` |
| char | 16 bits | Single characters | `char grade = 'A';` |
| boolean | 1 bit* | True/false values | `boolean isPassed = true;` |
 
*Note: While boolean logically needs only 1 bit, the actual storage size is JVM-dependent.
 

## Default Values

When you declare variables as class fields (instance or static variables), they get default values automatically:

```java
public class DefaultValues {
    // Numeric types default to 0
    byte b;      // 0
    short s;     // 0
    int i;       // 0
    long l;      // 0L
    float f;     // 0.0f
    double d;    // 0.0
    
    // char defaults to null character
    char c;      // '\u0000' (null character)
    
    // boolean defaults to false
    boolean bool; // false
}
```

**Important:** Local variables (declared inside methods) do **NOT** get default values - you must initialize them before use!

```java
public void localVariableExample() {
    int x;
    // System.out.println(x);  // ERROR! Must initialize before use
    
    x = 10;  // Now it's initialized
    System.out.println(x);  // OK
}
```