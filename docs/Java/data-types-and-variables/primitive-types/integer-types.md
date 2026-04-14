---
title: Integer Types
---

# Integers: Whole Numbers

Java provides four integer types, each with different sizes and ranges. All are **signed**, meaning they can be positive or negative.

## Why No Unsigned Integers?

Many languages have both signed and unsigned integers. Java's designers decided unsigned integers were unnecessary. Why?

The main use of unsigned integers in other languages was to control the behavior of the high-order bit (which normally indicates the sign). Java handles this differently with a special "unsigned right shift" operator (`>>>`), eliminating the need for separate unsigned types.


## The Integer Types

| Type    | Bits | Range                                    | Use Case |
|---------|------|------------------------------------------|----------|
| [byte](#byte-the-smallest-integer)    | 8    | -128 to 127                             | Binary data, streams, file I/O |
| [short](#short-the-rarely-used-type)   | 16   | -32,768 to 32,767                       | Rarely used in modern Java |
| [int](#int-the-workhorse)     | 32   | -2,147,483,648 to 2,147,483,647        | Default for whole numbers |
| [long](#long-for-really-big-numbers)    | 64   | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | Very large numbers |

---

## Understanding "Width"

When we talk about the "width" of an integer type, we mean the **behavior it defines**, not necessarily the physical storage it consumes. The JVM is free to use whatever storage it wants internally, as long as the type behaves according to its specification.

This is crucial for Java's portability: an `int` is **always** 32 bits in behavior, regardless of whether you're running on a phone, laptop, or server.

---

## `byte`: The Smallest Integer

```java
public class ByteDemo {
    public static void main(String[] args) {
        // byte range: -128 to 127
        byte minByte = -128;
        byte maxByte = 127;
        
        System.out.println("Byte range: " + minByte + " to " + maxByte);
        
        // Common use: reading binary data
        byte[] data = {65, 66, 67};  // ASCII codes for A, B, C
        for (byte b : data) {
            System.out.print((char) b);  // Convert to characters
        }
        System.out.println();
        
        // Overflow demonstration
        byte overflowTest = 127;
        overflowTest++;  // Wraps around to -128!
        System.out.println("127 + 1 = " + overflowTest);  // -128
    }
}
```

``` title="Output"
Byte range: -128 to 127
ABC
127 + 1 = -128
```

The `byte` type is perfect for:

- Reading data from networks or files
- Working with raw binary data
- Situations where you need to match external data formats
- Large arrays where memory is critical

---

## `short`: The Rarely Used Type

```java
public class ShortDemo {
    public static void main(String[] args) {
        // short range: -32,768 to 32,767
        short minShort = -32768;
        short maxShort = 32767;
        
        System.out.println("Short range: " + minShort + " to " + maxShort);
        
        // Why short is rarely used: automatic promotion to int
        short s1 = 100;
        short s2 = 200;
        
        // Result of arithmetic is int, not short!
        // short result = s1 + s2;  // ERROR: Cannot assign int to short
        
        // You need to cast back
        short result = (short) (s1 + s2);
        System.out.println("100 + 200 = " + result);
        
        // This makes int more convenient in most cases
        int betterResult = s1 + s2;  // No cast needed
        System.out.println("Using int instead: " + betterResult);
    }
}
```

```title="Output"
Short range: -32768 to 32767
100 + 200 = 300
Using int instead: 300
```

The `short` type is probably the **least-used** Java type. In most cases where you might think a short would save memory, an `int` works just as well due to how Java promotes types in expressions.

---


## `int`: The Workhorse

```java
public class IntDemo {
    public static void main(String[] args) {
        // int range: about ±2 billion
        int minInt = -2147483648;  // Or Integer.MIN_VALUE
        int maxInt = 2147483647;   // Or Integer.MAX_VALUE
        
        System.out.println("Int range: " + minInt + " to " + maxInt);
        
        // Most common uses
        int counter = 0;           // Loop counters
        int[] numbers = new int[100];  // Array indices
        int total = 0;             // Accumulators
        
        // Loop example
        for (int i = 0; i < 5; i++) {
            counter++;
            total += i;
        }
        System.out.println("Counter: " + counter + ", Total: " + total);
        
        // Overflow example - very important!
        int largeValue = 2147483647;
        System.out.println("Max int: " + largeValue);
        largeValue++;  // Overflows!
        System.out.println("Max int + 1: " + largeValue);  // -2147483648
        
        // Different number formats
        int decimal = 100;
        int hex = 0x64;      // Hexadecimal
        int binary = 0b1100100;  // Binary (Java 7+)
        int withUnderscores = 1_000_000;  // Readability (Java 7+)
        
        System.out.println("All represent 100: " + 
            (decimal == hex && hex == binary));
        System.out.println("One million: " + withUnderscores);
    }
}
```

``` title="Output"
Int range: -2147483648 to 2147483647
Counter: 5, Total: 10
Max int: 2147483647
Max int + 1: -2147483648
All represent 100: true
One million: 1000000
```

**Important behavior**: Even when you use `byte` or `short` in expressions, Java automatically promotes them to `int` during calculation. This makes `int` the natural choice for most integer operations.

---

## `long`: For Really Big Numbers

```java
public class LongDemo {
    public static void main(String[] args) {
        // long range: about ±9 quintillion
        long minLong = -9223372036854775808L;  // Or Long.MIN_VALUE
        long maxLong = 9223372036854775807L;   // Or Long.MAX_VALUE
        
        System.out.println("Long range:");
        System.out.println("Min: " + minLong);
        System.out.println("Max: " + maxLong);
        
        // Note the 'L' suffix for long literals
        long distance = 93000000L;  // Miles from Earth to Sun
        
        // Calculate light travel distance
        long lightSpeed = 186282L;  // Miles per second
        long secondsPerDay = 24L * 60L * 60L;
        long days = 1000L;
        
        long totalDistance = lightSpeed * secondsPerDay * days;
        System.out.println("\nLight travels in 1000 days:");
        System.out.println(totalDistance + " miles");
        System.out.println("That's " + (totalDistance / 1000000000) + " billion miles");
        
        // System timestamps use long
        long currentTime = System.currentTimeMillis();
        System.out.println("\nCurrent timestamp: " + currentTime);
        
        // File sizes often need long
        long fileSize = 5_000_000_000L;  // 5 GB in bytes
        System.out.println("Large file: " + fileSize + " bytes");
        
        // Overflow is still possible!
        long hugeValue = Long.MAX_VALUE;
        System.out.println("\nMax long: " + hugeValue);
        hugeValue++;
        System.out.println("Max long + 1: " + hugeValue);  // Wraps to minimum
    }
}
```


``` title="Output"
Long range:
Min: -9223372036854775808
Max: 9223372036854775807

Light travels in 1000 days:
16093286400000 miles
That's 16093 billion miles

Current timestamp: 1744877234567

Large file: 5000000000 bytes

Max long: 9223372036854775807
Max long + 1: -9223372036854775808
```

Use `long` when:

- Numbers exceed int's range (roughly ±2 billion)
- You need to avoid overflow in calculations
- Working with timestamps, large file sizes, or astronomical numbers
- Dealing with unique IDs that need wide range

---

## Type Promotion in Expressions

```java
public class TypePromotion {
    public static void main(String[] args) {
        // Java promotes smaller types to int in expressions
        byte b1 = 10;
        byte b2 = 20;
        
        // The result is int, not byte!
        // byte result = b1 + b2;  // ERROR!
        int result = b1 + b2;      // OK
        
        // This applies to all operations
        short s = 100;
        byte b = 50;
        // short mixedResult = s + b;  // ERROR: result is int
        
        // When mixing types, the smaller promotes to larger
        int i = 100;
        long l = 1000L;
        long mixedLong = i + l;  // int promoted to long
        
        // Demonstration
        System.out.println("byte + byte = int: " + result);
        System.out.println("int + long = long: " + mixedLong);
        
        // Useful rule: anything smaller than int becomes int in calculations
        byte tiny = 1;
        int bigger = tiny * 2;  // Multiplication produces int
        System.out.println("Result: " + bigger);
    }
}
```

``` title="Output"
byte + byte = int: 30
int + long = long: 1100
Result: 2
```

---

## Integer Literals: Special Notations

```java
public class IntegerLiterals {
    public static void main(String[] args) {
        // Decimal (base 10) - default
        int decimal = 255;
        
        // Hexadecimal (base 16) - prefix 0x or 0X
        int hex = 0xFF;  // Same as 255
        
        // Binary (base 2) - prefix 0b or 0B
        int binary = 0b11111111;  // Same as 255
        
        // Octal (base 8) - prefix 0 (avoid this, it's confusing!)
        int octal = 0377;  // Same as 255
        
        // All are the same value
        System.out.println("Decimal: " + decimal);
        System.out.println("Hex: " + hex);
        System.out.println("Binary: " + binary);
        System.out.println("Octal: " + octal);
        System.out.println("All equal? " + 
            (decimal == hex && hex == binary && binary == octal));
        
        // Underscores for readability (Java 7+)
        int million = 1_000_000;
        int binary32 = 0b0100_1101_0110_1111;
        long creditCard = 1234_5678_9012_3456L;
        
        System.out.println("\nReadable numbers:");
        System.out.println("Million: " + million);
        System.out.println("Binary: " + binary32);
        System.out.println("Card: " + creditCard);
    }
}
```

``` title="Output"
Decimal: 255
Hex: 255
Binary: 255
Octal: 255
All equal? true

Readable numbers:
Million: 1000000
Binary: 19823
Card: 1234567890123456
```

---

## Common Pitfalls and Best Practices

### Pitfall 1: Integer Overflow

```java
public class OverflowPitfall {
    public static void main(String[] args) {
        // Silent overflow - no error!
        int a = 2_000_000_000;
        int b = 2_000_000_000;
        int sum = a + b;  // Overflows!
        
        System.out.println("2 billion + 2 billion = " + sum);  // Negative!
        
        // Solution: Use long when needed
        long correctSum = (long) a + (long) b;
        System.out.println("Correct sum: " + correctSum);
        
        // Or detect overflow
        try {
            int checkedSum = Math.addExact(a, b);  // Throws exception
        } catch (ArithmeticException e) {
            System.out.println("Overflow detected!");
        }
    }
}
```


### Pitfall 2: Integer Division

```java
public class IntegerDivision {
    public static void main(String[] args) {
        // Integer division truncates!
        int result = 10 / 3;
        System.out.println("10 / 3 = " + result);  // 3, not 3.333...
        
        // To get decimal result, use double
        double correctResult = 10.0 / 3.0;
        System.out.println("10.0 / 3.0 = " + correctResult);
        
        // Or cast one operand
        double alsoCorrect = (double) 10 / 3;
        System.out.println("(double) 10 / 3 = " + alsoCorrect);
    }
}
```



### Best Practice: Use the Right Type

```java
public class ChooseRightType {
    public static void main(String[] args) {
        // Use int for most integer needs
        int counter = 0;
        int arraySize = 100;
        int age = 25;
        
        // Use long when values might exceed ±2 billion
        long timestamp = System.currentTimeMillis();
        long fileSize = 5_000_000_000L;
        long population = 8_000_000_000L;
        
        // Use byte for raw binary data
        byte[] data = {0x48, 0x65, 0x6C, 0x6C, 0x6F};  // "Hello"
        
        // Avoid short unless you have a specific reason
        // (it's not more efficient and requires casts)
        
        System.out.println("Chose appropriate types!");
    }
}
```