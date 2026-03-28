# Java Loops and Jump Statements

### 1. Iteration and Why Loops Exist
* **Sequential Flow:** Typically, code executes line-by-line from top to bottom.
* **Control Flow (Branching):** Conditional statements like `if-else` split the execution path into different routes depending on conditions.
* **Iteration (Loops):** Loops exist to solve the problem of redundancy. If a specific block of code needs to be executed repeatedly (e.g., printing numbers from 1 to 10), it is highly inefficient to write 10 individual print statements. Loops handle this by iterating over the same block of code for a predefined number of times or until a certain condition is met.

---

### 2. The `while` Loop
* **Structure:**
    ```java
    while (boolean_expression) {
        // Execute this block
    }
    ```
* **When & Why to Use It:** Best used when the number of iterations is not known in advance, and the execution heavily relies on a dynamic condition being `true`. 
* **Flow:** It is an **entry-controlled** loop. It checks the boolean condition *first*. If it is `true`, it enters the loop body. If the initial condition is `false`, the code block inside will *never* execute.

---

### 3. The `do-while` Loop
* **Structure:**
    ```java
    do {
         // Execute this block
    } while (boolean_expression);
    ```
* **Difference from `while` Loop:** The `do-while` loop is **exit-controlled**. It performs the work inside the code block *first*, and only checks the condition at the end of the execution. 
* **When & Why to Use It:** Because it guarantees that the loop body will execute **at least once** regardless of the condition, it is the standard choice for **Menu Item Selections** (e.g., showing a user a game menu with "Play", "Load", "Exit" before evaluating their input). 

---

### 4. The `for` Loop 
* **Structure:**
    ```java
    for (initialization; condition; increment/decrement) {
        // Execute this block
    }
    ```
* **Real Execution Flow Tracing Step-by-Step:**
    1.  **Initialization:** The loop defines and sets the starting value of the control variable (e.g., `int i = 1`). This step happens **only once** at the very beginning.
    2.  **Condition Evaluation:** The program checks the boolean expression (e.g., `i <= 10`). If `true`, it proceeds into the loop body. If `false`, the loop completely terminates.
    3.  **Body Execution:** The code block inside the `{ }` brackets executes.
    4.  **Increment/Decrement:** Once the body finishes executing, the flow of control jumps directly back up to the increment/decrement statement (e.g., `i++`).
    5.  **Repeat:** The program goes back to **Step 2** to re-evaluate the condition. This cycle loops until the condition becomes `false`.
* **Advanced usage (Comma-separated variables):** You can manage multiple variables inside a single `for` loop initialization and increment block. 
    * *Example:* `for(int i = 1, j = 1; i <= 10 && j <= 5; i++, j += 2)`

---

### 5. Infinite Loops
* An infinite loop happens when a loop has no valid terminating condition, causing it to run endlessly until the system runs out of memory or the process is forcefully killed.
* **How they happen:**
    * **In a `while` loop:** Usually caused by forgetting to include an increment/decrement statement inside the loop body, meaning the evaluating variable never changes.
    * **In a `for` loop:** All parameters in a `for` loop are technically optional. Writing `for (;;) { ... }` or omitting the condition inherently creates an infinite loop.

---

### 6. Nested Loops
* A nested loop is simply a loop placed inside the body of another loop.
* **Execution Flow:** For *every single iteration* of the outer loop, the inner loop must start up and complete its *entire* lifecycle.
    * *Example:* If the outer loop is set to run 5 times, and the inner loop is set to run 5 times, the inner code block executes a total of 25 times ($5 \times 5$).
* **Primary Use Cases:** Traversing multi-dimensional arrays or solving **Pattern Printing** problems (e.g., generating right-angled triangles in the console using asterisk characters by linking the inner loop's condition to the outer loop's current iteration).

---

### 7. Jump Statements in Java
Jump statements disrupt the normal flow of control by forcibly transferring the execution sequence to another part of the program.

#### A. `break` Statement
* **Internal Working:** When the compiler hits a `break` keyword, it immediately destroys the current enclosing loop (or switch case block). The control flow jumps completely out of the loop and resumes at the next line of code *after* the loop block.
* **Use Cases:** Exiting a loop dynamically when a target is met. For example, if you are checking whether a number is prime by dividing it sequentially, you can `break` out of the loop the instant you find a valid divisor. There is no need to waste memory computing the remaining iterations.

#### B. `continue` Statement
* **How Control Skips Execution:** Instead of destroying the whole loop, `continue` just halts the **current iteration**. It skips any code left below it inside the block and forces the loop to instantly jump to the next iteration cycle.
    * **In a `for` loop:** It jumps to the increment/decrement phase.
    * **In a `while` loop:** It jumps to the boolean condition check.
* **Use Cases:** Selectively skipping values. For instance, if you want to print only odd numbers from 1 to 10, you can use `if (i % 2 == 0) continue;` to instantly skip the print statement for all even numbers.

#### C. Labeled Jump Statements (Bonus)
* If you have a nested loop scenario and you trigger a standard `break` inside the inner loop, it only exits the *inner* loop.
* Java allows you to name (label) loops (e.g., `outer: for(...)` and `inner: for(...)`).
* By writing **`break outer;`**, you can forcibly terminate the top-level outer loop directly from within an inner loop.