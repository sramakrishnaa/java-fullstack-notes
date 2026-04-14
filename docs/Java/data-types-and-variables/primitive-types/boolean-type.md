---
title: Boolean Type
---

# Boolean: True or False

## `boolean`: The Logical Type

```java
public class BooleanBasics {
    public static void main(String[] args) {
        // Declaring and initializing booleans
        boolean isJavaFun = true;
        boolean isFishTasty = false;
        
        System.out.println("Is Java fun? " + isJavaFun);
        System.out.println("Is fish tasty? " + isFishTasty);
        
        // Boolean from comparison
        int age = 20;
        boolean isAdult = age >= 18;
        System.out.println("Is adult? " + isAdult);
        
        // Boolean in conditions
        if (isJavaFun) {
            System.out.println("Let's write some Java!");
        }
        
        // Toggling boolean
        boolean flag = true;
        flag = !flag;  // Toggle using NOT operator
        System.out.println("Toggled flag: " + flag);
    }
}
```

``` title="Output"
Is Java fun? true
Is fish tasty? false
Is adult? true
Let's write some Java!
Toggled flag: false
```

The `boolean` type has only two possible values: `true` and `false`.

---

## What boolean is Used For

### 1. Relational Comparisons

```java
public class RelationalComparisons {
    public static void main(String[] args) {
        int a = 10;
        int b = 20;
        
        // Comparison operators return boolean
        boolean equal = (a == b);           // Equal to
        boolean notEqual = (a != b);        // Not equal to
        boolean lessThan = (a < b);         // Less than
        boolean lessOrEqual = (a <= b);     // Less than or equal
        boolean greaterThan = (a > b);      // Greater than
        boolean greaterOrEqual = (a >= b);  // Greater than or equal
        
        System.out.println("a = " + a + ", b = " + b);
        System.out.println("a == b: " + equal);
        System.out.println("a != b: " + notEqual);
        System.out.println("a < b: " + lessThan);
        System.out.println("a <= b: " + lessOrEqual);
        System.out.println("a > b: " + greaterThan);
        System.out.println("a >= b: " + greaterOrEqual);
    }
}
```


``` title="Output"  
a = 10, b = 20
a == b: false
a != b: true
a < b: true
a <= b: true
a > b: false
a >= b: false
```


### 2. Control Flow

```java
public class ControlFlow {
    public static void main(String[] args) {
        int score = 85;
        boolean passed = score >= 60;
        
        // if statement
        if (passed) {
            System.out.println("Congratulations! You passed.");
        } else {
            System.out.println("Sorry, you failed.");
        }
        
        // while loop
        int count = 0;
        boolean keepGoing = true;
        while (keepGoing) {
            System.out.println("Count: " + count);
            count++;
            if (count >= 3) {
                keepGoing = false;
            }
        }
        
        // for loop with boolean condition
        for (int i = 0; i < 5; i++) {
            boolean isEven = (i % 2 == 0);
            System.out.println(i + " is even: " + isEven);
        }
        
        // do-while
        int x = 0;
        do {
            System.out.println("x = " + x);
            x++;
        } while (x < 3);
    }
}
```

``` title="Output"
Congratulations! You passed.
Count: 0
Count: 1
Count: 2
0 is even: true
1 is even: false
2 is even: true
3 is even: false
4 is even: true
x = 0
x = 1
x = 2
```


### 3. Logical Operations

```java
public class LogicalOperations {
    public static void main(String[] args) {
        boolean a = true;
        boolean b = false;
        
        // Logical AND (&&) - both must be true
        boolean andResult = a && b;
        System.out.println("true && false = " + andResult);
        
        // Logical OR (||) - at least one must be true
        boolean orResult = a || b;
        System.out.println("true || false = " + orResult);
        
        // Logical NOT (!) - inverts the value
        boolean notResult = !a;
        System.out.println("!true = " + notResult);
        
        // Complex expressions
        int age = 25;
        boolean hasLicense = true;
        boolean canDrive = (age >= 18) && hasLicense;
        System.out.println("\nCan drive: " + canDrive);
        
        // Multiple conditions
        int temperature = 75;
        boolean isComfortable = (temperature >= 65) && (temperature <= 80);
        System.out.println("Temperature comfortable: " + isComfortable);
        
        // Combining AND and OR
        boolean isWeekend = true;
        boolean isHoliday = false;
        boolean canRelax = isWeekend || isHoliday;
        System.out.println("Can relax: " + canRelax);
    }
}
```


``` title="Output"
true && false = false
true || false = true
!true = false

Can drive: true
Temperature comfortable: true
Can relax: true
```

---


## Key Takeaways
 
✅ DO:

- Use boolean for true/false conditions
- Name boolean variables as questions: `isValid`, `hasPermission`, `canAccess`
- Use logical operators: `&&`, `||`, `!`
- Return boolean from methods that check conditions
 
❌ DON'T:

- Try to use integers as booleans (not allowed in Java)
- Compare boolean with `== true` (redundant: just use the variable)
- Use magic numbers for boolean-like values (use actual booleans)
 
```java
// Good boolean usage
boolean isValid = (x > 0);
if (isValid) {
    // Do something
}
 
// Bad boolean usage
// if (isValid == true) {  // Redundant!
if (isValid) {  // Better!
    // Do something
}
```
 
**Remember**: In Java, boolean is a distinct type with only two values: `true` and `false`. It cannot be confused with integers or any other type!