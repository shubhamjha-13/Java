# Java Functions Deep Dive | Detailed Notes

### 1. What are Functions in Java?
A function in Java is an independent block of code designed to perform a specific task. It can be compared to a mathematical function, $f(x)$, where you provide an input, the function processes that input, and then it produces an output. In Java, once we move to Object-Oriented Programming (OOP), functions that belong to a class are often referred to as **methods**.

### 2. Why do we need Functions?
The primary reason for using functions is **code reusability**. 
* Imagine a scenario where you need to add two numbers multiple times throughout your program. Without functions, you would have to write the variable declarations and addition logic over and over again. 
* By creating an `add` function, you simply write the logic once and **call** the function whenever you need to add numbers. This makes the code cleaner, easier to maintain, and prevents repetitive boilerplate code.

### 3. Types of Functions
Functions can be categorized into four types based on whether they take inputs (parameters) and whether they return an output:
1. **No Input, No Output:** The function takes no parameters and returns nothing (uses the `void` keyword).
2. **Input, No Output:** The function takes parameters to process but does not return a value back to the caller.
3. **No Input, Output:** The function takes no parameters but returns a value (e.g., a function that simply generates and returns a random number or a fixed value).
4. **Input and Output:** The function takes parameters, processes them, and returns a computed result.

### 4. How to Define Functions in Code
When defining a function, it is written outside of the `main` method block but inside the class. 

Here is the standard syntax:
```java
static returnType functionName(parameters) {
    // Code block to execute
    return value; // (Optional if returnType is void)
}
```

**Example of an Input & Output function:**
```java
public class Demo {
    // Function definition
    static int sum(int a, int b) {  // 'a' and 'b' are parameters
        int result = a + b;
        return result; 
    }

    public static void main(String[] args) {
        // Calling the function
        int x = sum(4, 5); // '4' and '5' are arguments
        System.out.println(x); // Prints 9
    }
}
```
* **Parameters vs. Arguments:** `int a` and `int b` in the function definition are **parameters** (the variables expecting data). When the function is actually called via `sum(4, 5)`, `4` and `5` are the **arguments** (the actual values passed in).
* **Return Type:** If a function returns an integer, the return type is `int`. If it returns nothing, the return type is `void`. 

### 5. Understanding the Main Method
You have actually been using a function all along: the `main` method! 
```java
public static void main(String[] args) { ... }
```
* **It is a function:** `main` is the name of the function, `void` is its return type, and `String[] args` is the parameter it takes. 
* **Entry Point:** The Java Virtual Machine (JVM) actively looks for the `main` function to start executing your program. If you write functions outside of `main` but never call them *inside* `main`, they will never be executed.

### 6. Function Overloading (Compile-Time Polymorphism)
Function Overloading allows you to have multiple functions with the **exact same name** in the same class, as long as their parameters are different. The compiler figures out which function to execute based on the arguments you pass during the function call.

You can overload functions by changing:
1. **The Number of Parameters:** e.g., `sum(int a, int b)` vs `sum(int a, int b, int c)`.
2. **The Types of Parameters:** e.g., `sum(int a, int b)` vs `sum(double a, double b)`.
3. **The Order of Parameters:** e.g., `greet(String name, int age)` vs `greet(int age, String name)`.

**Important Rule:** You **cannot** overload a function by *only* changing its return type (e.g., having an `int sum()` and a `void sum()`). The compiler will throw an error because if you don't assign the returned value to a variable during the call, the compiler won't know which version of the function you intended to execute.

### 7. Function Chaining
Function chaining (or the Call Stack flow) happens when one function calls another function, which in turn can call another.
* **Execution Flow:** If `main` calls Function A, and Function A calls Function B. The execution of Function A pauses, and the system jumps into Function B. Once Function B finishes executing and returns, the system goes back to Function A, picks up exactly where it left off, and finishes it before finally returning to `main`.

### 8. Scope: Local and Global
* **Local Scope:** Any variable declared inside a block of code (between `{` and `}` curly braces) is only accessible within that specific block. If you declare `int x = 5` inside an `if` statement or a specific function, it gets destroyed from memory once that block finishes executing. Another function cannot access that `x`.
* **Global Scope:** If you declare a variable outside of all functions but inside the class definition (e.g., `static String name = "Aditya";`), it becomes globally accessible to any function within that file/class.

### 9. Recursion Explained with Code
Recursion occurs when a **function calls itself**. It is an elegant way to solve complex problems by breaking them down into smaller sub-problems (highly utilized in Data Structures and Algorithms).

**Crucial Components of Recursion:**
1. **Recursive Call:** The function calling itself with a modified parameter.
2. **Base Case:** A strict condition that stops the recursion. Without a base case, the function will call itself infinitely, crashing the program.

**Example: Printing numbers from 5 down to 1 using recursion**
```java
public class Demo {
    static void printNum(int n) {
        // 1. Base Case: stops the recursion
        if (n == 0) {
            return; 
        }
        
        // Output the current number
        System.out.println(n);
        
        // 2. Recursive Call: calls itself with a reduced number
        printNum(n - 1); 
    }

    public static void main(String[] args) {
        printNum(5); 
    }
}
```
* **How it works:** `printNum(5)` prints 5, then calls `printNum(4)`. That prints 4, and calls `printNum(3)`, and so on. Once `printNum(0)` is called, the `if (n == 0)` condition hits, the function executes `return;` (stopping the chain), and the stack unrolls back to the main method.