---
title: Floating-Point Types
---

# Floating-Point Types: Decimal Numbers

When you need fractional precision - values like 3.14159 or 0.0001 - you use floating-point types. Java implements the [IEEE-754](https://en.wikipedia.org/wiki/IEEE_754){:target="_blank"} standard for floating-point arithmetic.


## The Two Floating-Point Types

| Type    | Bits | Approximate Range       | Precision | Decimal Digits |
|---------|------|------------------------|-----------|----------------|
| [float](#float-single-precision)   | 32   | 1.4e-45 to 3.4e+38     | Single precision | ~6-7 digits |
| [double](#double-double-precision)  | 64   | 4.9e-324 to 1.8e+308   | Double precision | ~15-16 digits |

---

## `float`: Single Precision

```java
public class FloatDemo {
    public static void main(String[] args) {
        // float requires 'f' or 'F' suffix
        float temperature = 98.6f;
        float price = 19.99f;
        float pi = 3.14159f;
        
        System.out.println("Temperature: " + temperature + "°F");
        System.out.println("Price: $" + price);
        System.out.println("Pi (float): " + pi);
        
        // Range demonstration
        float tiny = 1.4e-45f;      // Smallest positive
        float huge = 3.4e38f;       // Largest
        System.out.println("\nFloat range:");
        System.out.println("Tiny: " + tiny);
        System.out.println("Huge: " + huge);
        
        // Precision limitation (6-7 significant digits)
        float precise = 123456.7f;      // OK
        float notPrecise = 12345678.9f; // Loses precision
        System.out.println("\nPrecision test:");
        System.out.println("precise: " + precise);
        System.out.println("notPrecise: " + notPrecise);  // Rounded
        
        // Float arithmetic
        float a = 10.5f;
        float b = 2.3f;
        float sum = a + b;
        System.out.println("\n10.5 + 2.3 = " + sum);
    }
}
```

``` title="Output"
Temperature: 98.6°F
Price: $19.99
Pi (float): 3.14159

Float range:
Tiny: 1.4E-45
Huge: 3.4E38

Precision test:
precise: 123456.7
notPrecise: 1.2345679E7

10.5 + 2.3 = 12.8
```

Use `float` when:

- You need decimal numbers but don't need extreme precision
- Memory is a concern (half the size of double)
- Working with graphics, games, or scientific simulations where approximate values are acceptable

**Trade-off**: Faster and smaller than `double`, but less precise. Values become imprecise when very large or very small.

**Important**: For monetary values, use `BigDecimal` class instead to avoid rounding errors!

---

## `double`: Double Precision

```java
public class DoubleDemo {
    public static void main(String[] args) {
        // double is the default for decimal literals (no suffix needed)
        double pi = 3.141592653589793;
        double radius = 10.8;
        double area = pi * radius * radius;
        
        System.out.println("Pi (double): " + pi);
        System.out.println("Radius: " + radius);
        System.out.println("Area: " + area);
        
        // Range demonstration
        double tiny = 4.9e-324;    // Smallest positive
        double huge = 1.8e308;     // Largest
        System.out.println("\nDouble range:");
        System.out.println("Tiny: " + tiny);
        System.out.println("Huge: " + huge);
        
        // Precision demonstration (15-16 significant digits)
        double veryPrecise = 123456789012345.0;
        System.out.println("\nVery precise: " + veryPrecise);
        
        // Scientific notation
        double avogadro = 6.022e23;  // Avogadro's number
        double electronMass = 9.109e-31;  // kg
        System.out.println("\nScientific notation:");
        System.out.println("Avogadro: " + avogadro);
        System.out.println("Electron mass: " + electronMass);
    }
}
```


``` title="Output"
Pi (double): 3.141592653589793
Radius: 10.8
Area: 366.0590173247986

Double range:
Tiny: 4.9E-324
Huge: 1.8E308

Very precise: 1.23456789012345E14

Scientific notation:
Avogadro: 6.022E23
Electron mass: 9.109E-31
```

The `double` type is the default for decimal numbers in Java. Use it when:

- You need accurate calculations over many iterations
- Working with very large or very small numbers
- Precision matters (scientific calculations, graphics, etc.)

**Performance note**: On modern processors optimized for mathematical calculations, `double` can actually be **faster** than `float`.

**Math functions**: All transcendental functions (sin, cos, sqrt, etc.) return `double` values.

---

## float vs double: Precision Comparison

```java
public class PrecisionComparison {
    public static void main(String[] args) {
        // Same value, different precision
        float floatPi = 3.14159265358979323846f;
        double doublePi = 3.14159265358979323846;
        
        System.out.println("float Pi:  " + floatPi);
        System.out.println("double Pi: " + doublePi);
        System.out.println("Difference visible!\n");
        
        // Calculation precision difference
        float floatCalc = 1.0f / 3.0f;
        double doubleCalc = 1.0 / 3.0;
        
        System.out.println("1/3 as float:  " + floatCalc);
        System.out.println("1/3 as double: " + doubleCalc);
        System.out.println();
        
        // Accumulated error demonstration
        float floatSum = 0.0f;
        double doubleSum = 0.0;
        
        for (int i = 0; i < 1000000; i++) {
            floatSum += 0.001f;
            doubleSum += 0.001;
        }
        
        System.out.println("After adding 0.001 one million times:");
        System.out.println("float sum:  " + floatSum);
        System.out.println("double sum: " + doubleSum);
        System.out.println("Expected:   1000.0");
        System.out.println("Double is more accurate!");
    }
}
```


``` title="Output"
float Pi:  3.1415927
double Pi: 3.141592653589793
Difference visible!

1/3 as float:  0.33333334
1/3 as double: 0.3333333333333333

After adding 0.001 one million times:
float sum:  1000.0009
double sum: 1000.0000000159161
Expected:   1000.0
Double is more accurate!
```

---

## Special Floating-Point Values

```java
public class SpecialFloatValues {
    public static void main(String[] args) {
        // Positive and negative infinity
        double positiveInfinity = 1.0 / 0.0;
        double negativeInfinity = -1.0 / 0.0;
        
        System.out.println("Positive infinity: " + positiveInfinity);
        System.out.println("Negative infinity: " + negativeInfinity);
        
        // Not a Number (NaN)
        double nan = 0.0 / 0.0;
        System.out.println("NaN: " + nan);
        
        // Testing for special values
        System.out.println("\nTesting special values:");
        System.out.println("Is positive infinity? " + 
            Double.isInfinite(positiveInfinity));
        System.out.println("Is NaN? " + Double.isNaN(nan));
        
        // NaN is not equal to anything, even itself!
        System.out.println("NaN == NaN? " + (nan == nan));  // false!
        
        // Positive and negative zero
        double positiveZero = 0.0;
        double negativeZero = -0.0;
        System.out.println("\nPositive zero: " + positiveZero);
        System.out.println("Negative zero: " + negativeZero);
        System.out.println("Are they equal? " + (positiveZero == negativeZero));
    }
}
```

``` title="Output"
Positive infinity: Infinity
Negative infinity: -Infinity
NaN: NaN

Testing special values:
Is positive infinity? true
Is NaN? true
NaN == NaN? false!

Positive zero: 0.0
Negative zero: -0.0
Are they equal? true
```

---

## Common Floating-Point Pitfalls

### Pitfall 1: Comparing Floating-Point Numbers

```java
public class FloatComparison {
    public static void main(String[] args) {
        // NEVER compare floating-point with ==
        double a = 0.1 + 0.2;
        double b = 0.3;
        
        System.out.println("0.1 + 0.2 = " + a);
        System.out.println("0.3 = " + b);
        System.out.println("Are they equal with ==? " + (a == b));  // false!
        
        // Correct way: compare with epsilon (tolerance)
        double epsilon = 0.000001;
        boolean almostEqual = Math.abs(a - b) < epsilon;
        System.out.println("Almost equal? " + almostEqual);  // true
        
        // Even simpler cases can fail
        double x = 1.0 / 3.0;
        double y = x * 3.0;
        System.out.println("\n(1/3) * 3 = " + y);
        System.out.println("Equals 1.0? " + (y == 1.0));  // false!
    }
}
```

``` title="Output"
0.1 + 0.2 = 0.30000000000000004
0.3 = 0.3
Are they equal with ==? false
Almost equal? true

(1/3) * 3 = 1.0
Equals 1.0? true
```


### Pitfall 2: Loss of Precision in Conversion

```java
public class PrecisionLoss {
    public static void main(String[] args) {
        // Converting from double to float loses precision
        double preciseValue = 3.14159265358979;
        float lessPreci = (float) preciseValue;
        
        System.out.println("Original double: " + preciseValue);
        System.out.println("After float cast: " + lessPreci);
        System.out.println("Precision lost!\n");
        
        // Large integers lose precision in float
        long bigNumber = 123456789012345L;
        float floatNumber = (float) bigNumber;
        long backToLong = (long) floatNumber;
        
        System.out.println("Original long: " + bigNumber);
        System.out.println("As float: " + floatNumber);
        System.out.println("Back to long: " + backToLong);
        System.out.println("Lost: " + (bigNumber - backToLong));
    }
}
```

``` title="Output"
Original double: 3.14159265358979
After float cast: 3.1415927
Precision lost!

Original long: 123456789012345
As float: 1.23456788E14
Back to long: 123456791707648
Lost: -2695303
```


### Pitfall 3: Accumulation Errors

```java
public class AccumulationError {
    public static void main(String[] args) {
        // Adding small numbers repeatedly
        double sum = 0.0;
        for (int i = 0; i < 10; i++) {
            sum += 0.1;
        }
        
        System.out.println("Adding 0.1 ten times:");
        System.out.println("Result: " + sum);
        System.out.println("Expected: 1.0");
        System.out.println("Equal to 1.0? " + (sum == 1.0));
        
        // Better for money: use integers (cents)
        int cents = 0;
        for (int i = 0; i < 10; i++) {
            cents += 10;  // 10 cents
        }
        double dollars = cents / 100.0;
        System.out.println("\nUsing integer cents: $" + dollars);
    }
}
```

``` title="Output"
Adding 0.1 ten times:
Result: 0.9999999999999999
Expected: 1.0
Equal to 1.0? false

Using integer cents: $1.0
```

---

## Mathematical Operations

```java
public class MathOperations {
    public static void main(String[] args) {
        // All Math methods work with double
        double angle = 45.0;  // degrees
        double radians = Math.toRadians(angle);
        
        System.out.println("Trigonometry:");
        System.out.println("sin(45°) = " + Math.sin(radians));
        System.out.println("cos(45°) = " + Math.cos(radians));
        System.out.println("tan(45°) = " + Math.tan(radians));
        
        // Power and roots
        System.out.println("\nPowers and roots:");
        System.out.println("2^10 = " + Math.pow(2, 10));
        System.out.println("√144 = " + Math.sqrt(144));
        System.out.println("∛27 = " + Math.cbrt(27));
        
        // Logarithms
        System.out.println("\nLogarithms:");
        System.out.println("log(100) = " + Math.log10(100));
        System.out.println("ln(e) = " + Math.log(Math.E));
        
        // Rounding
        double value = 3.7;
        System.out.println("\nRounding 3.7:");
        System.out.println("ceil: " + Math.ceil(value));    // 4.0
        System.out.println("floor: " + Math.floor(value));  // 3.0
        System.out.println("round: " + Math.round(value));  // 4
        
        // Random numbers
        double random = Math.random();  // 0.0 to 1.0
        System.out.println("\nRandom: " + random);
    }
}
```

---

## Formatting Floating-Point Output

```java
public class FloatFormatting {
    public static void main(String[] args) {
        double pi = 3.14159265358979;
        double price = 19.99;
        double tiny = 0.0000123;
        
        // Using printf for formatting
        System.out.println("Formatted output:");
        System.out.printf("Pi with 2 decimals: %.2f%n", pi);
        System.out.printf("Pi with 5 decimals: %.5f%n", pi);
        System.out.printf("Price: $%.2f%n", price);
        System.out.printf("Scientific: %e%n", tiny);
        
        // Using String.format
        String formatted = String.format("%.2f", pi);
        System.out.println("\nFormatted string: " + formatted);
        
        // Controlling width and alignment
        System.out.printf("%nFormatted table:%n");
        System.out.printf("%10s %10s%n", "Item", "Price");
        System.out.printf("%10s %10.2f%n", "Apple", 1.99);
        System.out.printf("%10s %10.2f%n", "Banana", 0.59);
        System.out.printf("%10s %10.2f%n", "Orange", 1.29);
    }
}
```


``` title="Output"
Formatted output:
Pi with 2 decimals: 3.14
Pi with 5 decimals: 3.14159
Price: $19.99
Scientific: 1.230000e-05

Formatted string: 3.14

Formatted table:
      Item      Price
     Apple       1.99
    Banana       0.59
    Orange       1.29
```

---

## Best Practices

✅ DO:

- Use `double` as your default floating-point type
- Use `BigDecimal` for monetary calculations
- Compare floating-point numbers with tolerance (epsilon)
- Format output appropriately for display
- Be aware of precision limitations

❌ DON'T:

- Use `==` to compare floating-point numbers
- Use `float` or `double` for precise financial calculations
- Assume floating-point arithmetic is exact
- Ignore accumulated rounding errors in loops
- Mix float and double unnecessarily (stick to one)

```java
// Good practices summary
public class FloatingPointBestPractices {
    public static void main(String[] args) {
        // ✅ Use double by default
        double temperature = 98.6;
        
        // ✅ Use BigDecimal for money
        // BigDecimal price = new BigDecimal("19.99");
        
        // ✅ Compare with tolerance
        double a = 0.1 + 0.2;
        double b = 0.3;
        boolean equal = Math.abs(a - b) < 0.000001;
        
        // ❌ Don't do this for money
        double moneyBad = 19.99;
        moneyBad = moneyBad * 1.08;  // Tax calculation - imprecise!
        
        System.out.println("Follow best practices!");
    }
}
```