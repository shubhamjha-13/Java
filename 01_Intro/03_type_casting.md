# Java Type Conversion Notes

## 1. Implicit (Widening) Type Conversion
Implicit conversion happens automatically when you assign a value of a smaller data type to a larger data type. Because the destination is "wider" than the source (e.g., a 32-bit int can easily hold an 8-bit byte), there is no risk of data loss, so the Java compiler handles it for you.

```java
// Example: byte to int [00:19:16]
byte b = 24;
int i = b; // Automatically widened from 8-bit to 32-bit
System.out.println(i); // Outputs: 24

// Example: char to int [00:19:57]
char c = 'a';
int asciiValue = c; // 'a' has a Unicode value of 97
System.out.println(asciiValue); // Outputs: 97
```

## 2. Explicit (Narrowing) Type Casting
Explicit conversion is required when you try to assign a larger data type to a smaller one (e.g., a 32-bit int to an 8-bit byte). Because the smaller container might not be able to hold the larger value, the Java compiler will throw an error to protect you. You must explicitly tell the compiler to perform the conversion by using a cast (`(type)`).

```java
// Example: int to byte [00:20:58]
int i = 24;
// byte b = i; // ERROR: Type mismatch: cannot convert from int to byte
byte b = (byte) i; // Explicitly casting int to byte
System.out.println(b); // Outputs: 24
```

## 3. Data Loss & Truncation
When you perform explicit (narrowing) casting, data loss or truncation can occur if the original value exceeds the maximum capacity of the target data type.

- **Modulo/Binary Truncation:** If you cast an int (like 300) into a byte (which can only hold -128 to 127), Java looks at the binary representation of 300 and chops off all but the first 8 bits. Mathematically, this is the same as taking the number modulo the total range of a byte (300 % 256 = 44).
- **Decimal Truncation:** When converting floating-point numbers (float or double) to integers, the decimal portion is completely discarded, not rounded.

```java
// Example: Value out of range (Modulo Truncation) [00:21:55]
int largeInt = 300;
byte truncatedByte = (byte) largeInt; 
System.out.println(truncatedByte); // Outputs: 44 (because 300 % 256 = 44)

// Example: Decimal Truncation [00:23:06]
float f = 15.678f;
int truncatedInt = (int) f;
System.out.println(truncatedInt); // Outputs: 15 (decimals are dropped)
```

## 4. Why boolean cannot be converted
In Java, `boolean` is a special data type that represents logical states (`true` or `false`). Unlike some other languages (like C++ or JavaScript) where `true` might equal 1 and `false` equals 0, Java treats booleans completely separately from numeric types. Therefore, you cannot implicitly or explicitly cast a `boolean` to an `int`, or vice versa.

```java
// Example: Boolean conversion attempt [00:24:45]
boolean bool = false;
// int i = bool; // ERROR: Type mismatch
// int i = (int) bool; // ERROR: Cannot cast from boolean to int
```

## 5. How Java handles arithmetic operations internally
When performing mathematical operations, Java calculates the result in an intermediate state. If you multiply two `byte` variables (e.g., `50 * 40`), the result is 2000, which heavily exceeds the maximum limit of a `byte` (127). To prevent the calculation from overflowing and crashing during runtime, Java automatically "promotes" the operands to an `int` before doing the math.

```java
// Example: Internal promotion during arithmetic [00:29:17]
byte b = 50;
// b = b * 2; // ERROR: b * 2 results in an int, which cannot be assigned back to a byte directly
b = (byte) (b * 2); // Correct: You must cast the int result back to a byte
System.out.println(b); // Outputs: 100
```

## 6. Type Promotion Rules in Expressions
When evaluating expressions, the Java compiler looks at the data types involved and automatically promotes them to the largest data type present in the operation to ensure enough memory is allocated for the result. The four strict rules are:

1. `byte`, `short`, and `char` are automatically promoted to `int` in any calculation.
2. If any one operand is a `long`, the entire expression evaluates to a `long`.
3. If any one operand is a `float`, the entire expression evaluates to a `float`.
4. If any one operand is a `double`, the entire expression evaluates to a `double`.

```java
// Example: Type Promotion Rules [00:34:52]
float f = 5.5f;
int i = 10;
double d = 20.5;

// The int 'i' is promoted to a float for the addition.
// The resulting float (15.5) is then promoted to a double for the subtraction.
double result = (f + i) - d;
```

## 7. Why char + char becomes int
Under the hood, Java stores characters as numeric Unicode values (e.g., `'A'` is stored as 65, `'a'` is stored as 97). Because of the first rule of Type Promotion (stated above), any arithmetic operation involving a `char` automatically promotes that `char` to an `int` before doing the math.

```java
// Example: char arithmetic
char c1 = 'A'; // Unicode 65
char c2 = 'B'; // Unicode 66

// c1 + c2 automatically promotes both to int: 65 + 66
int sum = c1 + c2; 
System.out.println(sum); // Outputs: 131
```