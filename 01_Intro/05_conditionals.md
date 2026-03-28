### **Flow of Control**
In programming, the "flow of control" refers to the order in which statements are executed when a program runs. 
* By default, Java executes code sequentially (line by line) from top to bottom.
* However, certain keywords can break this normal flow and redirect the execution based on conditions.
* Flow of control statements are primarily categorized into three types:
    1. **Selection (Decision Making):** Statements like `if`, `if-else`, and `switch`.
    2. **Iteration (Loops):** Statements like `for`, `while`, and `do-while`.
    3. **Jumps:** Statements like `break`, `continue`, and `return`.

---

### **Decision Making in Programming (Selection)**
Decision-making structures allow you to create forks in your code's path, much like coming to an intersection on a road and choosing which way to go based on specific criteria. In Java, this translates to evaluating an expression that yields a boolean value (`true` or `false`) and executing a specific block of code based on that result.

---

### **`if` Statement**
The `if` statement is the most basic selection statement. It tells the compiler to execute a block of code *only if* a specified condition evaluates to `true`.

* **Execution:** If the expression is `true`, the code inside the block runs. If it's `false`, the compiler skips the block entirely and continues with the next lines of the program.
* **Note:** Curly braces `{}` are optional if there is only one line of code inside the `if` block, but using them is highly recommended as a good coding practice to avoid confusion.

**Practical Example:**
```java
int i = 5;
if (i == 5) {
    System.out.println("i is exactly 5");
}
```

---

### **`if-else` Statement**
The `if-else` statement introduces a strict "either/or" path. 

* **Execution:** If the `if` expression evaluates to `true`, the first block executes. If it is `false`, the `else` block executes. Only one block will ever run.

**Practical Example:**
```java
int number = 9;
if (number % 2 == 0) {
    System.out.println("Number is Even");
} else {
    System.out.println("Number is Odd");
}
```

---

### **`if-else-if` Ladder**
When you have multiple, mutually exclusive conditions to check, you use an `if-else-if` ladder.

* **Execution flow:** The compiler checks conditions sequentially from top to bottom. 
* The moment it finds a `true` condition, it executes that specific block and immediately exits the entire ladder, skipping all subsequent checks.
* A final `else` block is often placed at the end to act as a default catch-all if none of the preceding conditions were met.

**Practical Example:**
```java
int age = 50;
if (age > 80) {
    System.out.println("You are very old");
} else if (age > 60) {
    System.out.println("You are old");
} else if (age > 40) {
    System.out.println("You are becoming old");
} else {
    System.out.println("You are young");
}
// For age = 50, it prints "You are becoming old" and skips the rest.
```

---

### **Nested `if` Statements**
You can place an `if` statement inside another `if` statement. This is known as nesting.

* It is used when a secondary condition needs to be checked only after a primary condition has already been validated.
* Each `if` block can have its own independent `else` block. 
* **Best Practice:** While Java allows infinite levels of nesting, deeply nested code becomes very difficult to read. It is usually better to combine conditions using logical operators (like `&&` or `||`) to keep the code clean and readable.

**Practical Example:**
```java
int i = 8;
if (i > 5) {
    if (i < 10) {
        System.out.println("i is between 5 and 10");
    }
}
// Better alternative: if (i > 5 && i < 10) { ... }
```

---

### **`switch` Statement**
The `switch` statement is an alternative to the `if-else-if` ladder, specifically designed to check a single variable against multiple potential, exact matches (called "cases").

* **The `break` Keyword:** In a `switch` block, if a case matches, the program starts executing code from that point downward. If you omit the `break` keyword, the code will "fall through" and execute all subsequent cases regardless of whether they match or not. `break` forces the compiler to exit the `switch` block immediately.
* **The `default` Keyword:** Acts like the final `else` in an `if-else` ladder. It executes if none of the cases match.
* **Nesting:** Just like `if` statements, `switch` statements can be nested inside one another, though it should be done sparingly to maintain readability.

**Practical Example:**
```java
int choice = 2;
switch (choice) {
    case 1:
        System.out.println("Choice is 1");
        break;
    case 2:
        System.out.println("Choice is 2");
        break;
    case 3:
        System.out.println("Choice is 3");
        break;
    default:
        System.out.println("Choice is greater than 3");
        break;
}
```

---

### **When to use `switch` vs `if-else-if`**
While both achieve similar results, they have different capabilities:

* **`if-else-if`:** Can evaluate complex boolean expressions, inequalities (`<`, `>`), and multiple variables at once. It can also handle duplicate conditions without throwing a compile error (though only the first true instance will execute).
* **`switch`:** Can *only* check for strict equality (`==`). Furthermore, the cases must be unique; duplicate cases will throw a compile-time error.
* **Data Types for Switch:** Historically, `switch` could only evaluate `byte`, `short`, `int`, `char`, and Enums. As of JDK 7, `String` is also supported. You **cannot** switch on a boolean value or an expression like `i > 4`.

---

### **Why `switch` can be more optimized (Internal Working Explanation)**
The `switch` statement is generally more optimized and faster than an `if-else-if` ladder because of how the Java compiler translates it into bytecode.

* **`if-else-if` is linear (O(n)):** It has to evaluate every single condition from the top down until it finds a match. If the match is at the very bottom (or is the `else` condition), it wastes time evaluating every single false condition above it.
* **`switch` uses Jump Tables (O(1) or O(log n)):** Instead of evaluating sequentially, the compiler analyzes the `switch` cases and creates a "Jump Table" under the hood.
    1. **Table Switch (Dense Values):** If your case values are close together or sequential (e.g., cases 1, 2, 3, 4), the compiler creates an internal array-like structure. It can immediately calculate the exact memory index of the matching code (e.g., `index = value - 1`) and jump straight to it. This takes O(1) time complexity, skipping sequential evaluations entirely.
    2. **Lookup Switch (Sparse Values):** If your case values are far apart (e.g., cases 1, 1000, 100000), creating a massive array would waste memory. Instead, the compiler creates a compact table of just the provided case values and uses a **Binary Search** algorithm to find the correct case quickly. This takes O(log n) time complexity, which is still vastly superior to the O(n) linear search of a long `if-else-if` ladder.