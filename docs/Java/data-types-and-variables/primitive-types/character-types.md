---
title: Character Type
---

# Characters: Unicode Support

## `char`: A 16-bit Character Type

```java hl_lines="5"
public class CharBasics {
    public static void main(String[] args) {
        // Different ways to create char
        char ch1 = 88;          // ASCII/Unicode code for 'X'
        char ch2 = 'Y';         // Character literal
        char ch3 = '\u005A';    // Unicode escape sequence for 'Z'
        
        System.out.println("ch1: " + ch1);  // X
        System.out.println("ch2: " + ch2);  // Y
        System.out.println("ch3: " + ch3);  // Z
        
        // char is a single character only
        // char word = "Hello";  // ERROR! String, not char
        char letter = 'H';       // OK: single character
        
        System.out.println("Single character: " + letter);
    }
}
```


``` title="Output"
ch1: X
ch2: Y
ch3: Z
Single character: H
```

Java uses **Unicode** to represent characters. This is a major design decision with important implications.

---

## Why Unicode?

Unicode is a unified character set that can represent characters from **all human languages**: English, Chinese, Arabic, Hebrew, Japanese, and many more.

**The cost of global support**: Unicode required 16 bits (at the time of Java's creation), making `char` a 16-bit type. This is somewhat inefficient for languages like English that need only 8 bits, but it's the price of portability.

**ASCII compatibility**: The first 127 values of Unicode match ASCII exactly, so all your familiar ASCII tricks still work.

---

## Unicode Escape Sequences

```java
public class UnicodeDemo {
    public static void main(String[] args) {
        // Unicode escape format: \uXXXX (4 hex digits)
        char heart = '\u2764';       // ❤
        char smiley = '\u263A';      // ☺
        char lambda = '\u03BB';      // λ (Greek)
        char omega = '\u03A9';       // Ω (Greek)
        
        System.out.println("Unicode symbols:");
        System.out.println("Heart: " + heart);
        System.out.println("Smiley: " + smiley);
        System.out.println("Lambda: " + lambda);
        System.out.println("Omega: " + omega);
        
        // International characters
        char chinese = '\u4E2D';     // 中 (Chinese: middle)
        char arabic = '\u0627';      // ا (Arabic letter)
        char hebrew = '\u05D0';      // א (Hebrew letter)
        
        System.out.println("\nInternational:");
        System.out.println("Chinese: " + chinese);
        System.out.println("Arabic: " + arabic);
        System.out.println("Hebrew: " + hebrew);
        
        // ASCII is just Unicode 0-127
        char asciiA = '\u0041';      // Same as 'A'
        char asciiZ = '\u005A';      // Same as 'Z'
        System.out.println("\nASCII via Unicode: " + asciiA + asciiZ);
    }
}
```


``` title="Output"
Unicode symbols:
Heart: ❤
Smiley: ☺
Lambda: λ
Omega: Ω

International:
Chinese: 中
Arabic: ا
Hebrew: א

ASCII via Unicode: AZ
```

---

## Escape Sequences

```java
public class EscapeSequences {
    public static void main(String[] args) {
        // Common escape sequences
        char newline = '\n';      // New line
        char tab = '\t';          // Tab
        char backslash = '\\';    // Backslash
        char singleQuote = '\'';  // Single quote
        char doubleQuote = '\"';  // Double quote
        char carriageReturn = '\r'; // Carriage return
        char backspace = '\b';    // Backspace
        char formFeed = '\f';     // Form feed
        
        System.out.println("Escape sequences:");
        System.out.println("Line 1" + newline + "Line 2");
        System.out.println("Column1" + tab + "Column2");
        System.out.println("Backslash: " + backslash);
        System.out.println("Quote: " + singleQuote);
        
        // Practical usage
        System.out.println("\nFormatted output:");
        System.out.println("Name:\tJohn");
        System.out.println("Age:\t25");
        System.out.println("City:\tNew York");
        
        // Path example
        String windowsPath = "C:\\Users\\Documents\\file.txt";
        System.out.println("\nPath: " + windowsPath);
    }
}
```


``` title="Output"
Escape sequences:
Line 1
Line 2
Column1	Column2
Backslash: \
Quote: '

Formatted output:
Name:	John
Age:	25
City:	New York

Path: C:\Users\Documents\file.txt
```

---

## char Can Act Like an Integer

Despite being for characters, `char` is technically an integral type. This means you can:

```java
public class CharArithmetic {
    public static void main(String[] args) {
        // Character arithmetic
        char ch = 'A';
        System.out.println("Starting char: " + ch);
        
        // Increment character
        ch++;
        System.out.println("After ch++: " + ch);  // B
        
        // Add to character
        ch = (char) (ch + 5);
        System.out.println("After +5: " + ch);    // G
        
        // Decrement
        ch--;
        System.out.println("After ch--: " + ch);  // F
        
        // Arithmetic operations
        char start = 'A';
        char end = 'Z';
        int difference = end - start;
        System.out.println("\nDistance from A to Z: " + difference);
        
        // Convert to uppercase/lowercase
        char lowercase = 'a';
        char uppercase = (char) (lowercase - 32);  // ASCII trick
        System.out.println("Lower: " + lowercase + ", Upper: " + uppercase);
        
        // Loop through characters
        System.out.print("\nFirst 10 letters: ");
        for (char c = 'A'; c <= 'J'; c++) {
            System.out.print(c + " ");
        }
        System.out.println();
    }
}
```


``` title="Output"
Starting char: A
After ch++: B
After +5: G
After ch--: F

Distance from A to Z: 25

Lower: a, Upper: A

First 10 letters: A B C D E F G H I J 
```

**Range**: 0 to 65,535 (no negative values - char is **unsigned**)

---

## ASCII Compatibility
 
```java
public class ASCIIDemo {
    public static void main(String[] args) {
        // First 128 characters of Unicode are ASCII
        System.out.println("Printable ASCII characters (32-126):\n");
        
        for (int i = 32; i <= 126; i++) {
            char c = (char) i;
            System.out.print(c);
            
            // New line every 40 characters
            if ((i - 32 + 1) % 40 == 0) {
                System.out.println();
            }
        }
        
        // ASCII control characters (0-31)
        System.out.println("\n\nSome ASCII control characters:");
        System.out.println("0: null character");
        System.out.println("9: tab");
        System.out.println("10: line feed (newline)");
        System.out.println("13: carriage return");
        
        // Common ASCII codes
        System.out.println("\nCommon ASCII codes:");
        System.out.println("'0' = " + (int) '0');  // 48
        System.out.println("'A' = " + (int) 'A');  // 65
        System.out.println("'a' = " + (int) 'a');  // 97
        System.out.println("' ' = " + (int) ' ');  // 32
    }
}
```

``` title="Output"
Printable ASCII characters (32-126):
 
 !"#$%&'()*+,-./0123456789:;<=>?
@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_
`abcdefghijklmnopqrstuvwxyz{|}~
 
Some ASCII control characters:
0: null character
9: tab
10: line feed (newline)
13: carriage return
 
Common ASCII codes:
'0' = 48
'A' = 65
'a' = 97
' ' = 32
```
 
---