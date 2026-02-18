#  1. Java Fundamentals: Hello World 


The classic entry point for any Java application.

```java
public class HelloWorld {
    public static void main(String[] args) {
        // Entry point for the JVM
        System.out.println("Hello, World!");
    }
}
```

---

#  2. Java Variables & Data Types

## 2.1 Variables in Java

A **variable** is a container (memory location) that holds data which can be changed during the execution of a program. In Java, every variable must be declared with a specific **Data Type** (Strongly Typed).

### 2.1.1 Syntax

```java
type variableName = value;
```
### 2.1.2 Strongly Typed Nature of Java

Java is **Strongly Typed**, meaning:

1. Every variable must have a declared **data type**.  
2. Type checking happens at **compile time**.
---

## 2.2 Data Types Hierarchy

Java data types are divided into two main categories:

1. **Primitive Data Types:** Store actual values (e.g., `int`, `boolean`).
2. **Non-Primitive (Reference) Data Types:** Store addresses/references to objects (e.g., `String`, `Array`, `Class`).

---

## 2.3 Primitive Data Types (The 8 Core Types)

Java has **8 built-in data types**. They are keywords and are stored directly in the **Stack memory** for fast access.

| Type | Description | Default Size | Default Value | Range / Notes |
| :--- | :--- | :--- | :--- | :--- |
| `byte` | Very small integer | 8-bit | `0` | -128 to 127 |
| `short` | Small integer | 16-bit | `0` | -32,768 to 32,767 |
| `int` | Standard integer | 32-bit | `0` | -2^31 to 2^31-1 (~2 billion) |
| `long` | Large integer | 64-bit | `0L` | -2^63 to 2^63-1 (Use suffix `L`) |
| `float` | Decimal (Single precision) | 32-bit | `0.0f` | 6-7 decimal digits (Use suffix `f`) |
| `double` | Decimal (Double precision) | 64-bit | `0.0d` | 15-16 decimal digits (Default for decimals) |
| `char` | Single character | 16-bit | `'\u0000'` | Stores a single Unicode character |
| `boolean` | True/False flag | ~1 bit | `false` | Only `true` or `false` |

---

#  3. Code Snippet: All 8 Primitive Types

```java
public class AllDataTypes {
    public static void main(String[] args) {
        
        // --- 1. Integer Types (Whole Numbers) ---
        byte smallNumber = 127;             // Max value for byte (-128 to 127)
        short shortNumber = 32000;          // Max ~32k
        int intNumber = 2147483647;         // Standard integer (Max ~2 billion)
        long longNumber = 9223372036854775807L; // Requires 'L' suffix for large numbers

        // --- 2. Floating-Point Types (Decimals) ---
        float floatNumber = 3.14159f;       // Requires 'f' suffix (otherwise treated as double)
        double doubleNumber = 3.1415926535; // Default for decimals (more precise)

        // --- 3. Character Type ---
        char letter = 'A';                  // Single character in single quotes
        char unicodeSymbol = '\u0024';      // Unicode value for '$'

        // --- 4. Boolean Type ---
        boolean isJavaFun = true;           // Only true or false

        // --- Output ---
        System.out.println("Byte:    " + smallNumber);
        System.out.println("Short:   " + shortNumber);
        System.out.println("Int:     " + intNumber);
        System.out.println("Long:    " + longNumber);
        System.out.println("Float:   " + floatNumber);
        System.out.println("Double:  " + doubleNumber);
        System.out.println("Char 1:  " + letter);
        System.out.println("Char 2:  " + unicodeSymbol);
        System.out.println("Boolean: " + isJavaFun);
    }
}
```