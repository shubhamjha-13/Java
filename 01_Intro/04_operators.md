### **Arithmetic Operators**
Arithmetic operators perform basic mathematical functions just as you would use them in algebra.
* **Basic Operations:** Addition (`+`), Subtraction (`-`), Multiplication (`*`), and Division (`/`).
* **Modulo (`%`):** Returns the remainder of a division operation rather than the quotient. For example, `10 % 5` yields `0`.
* **Compound Assignment:** You can combine arithmetic operations with the assignment operator (e.g., `+=`, `-=`, `*=`, `/=`, `%=`). This is a common shortcut to update a variable in place (e.g., `h += 2` is evaluated as `h = h + 2`).

### **Unary Operators**
Unlike binary operators (which require two operands, like `a + b`), unary operators require only a single operand. Common examples include logical NOT (`!`), bitwise NOT (`~`), and the increment/decrement operators.

### **Increment & Decrement (Pre vs Post)**
These operators are shorthand for adding or subtracting 1 from a variable's current value.
* **Pre-Increment/Decrement (`++j` / `--j`):** The variable's value is modified *first*, and then that newly updated value is assigned to the expression.
* **Post-Increment/Decrement (`j++` / `j--`):** The expression gets evaluated using the variable's *current* value first, and the modification happens *afterward*.
* **Interview Trap / Internal Evaluation:** If you execute `k = j++` (where `j` is initially `9`), `k` will be assigned `9`, while `j` becomes `10` internally. Conversely, `l = ++j` will result in both `l` and `j` becoming `11`.

### **Relational Operators**
Relational operators compare two variables and output a `boolean` result (`true` or `false`).
* **Comparisons:** They include strict equality (`==`), inequality (`!=`), less than (`<`), greater than (`>`), less than or equal to (`<=`), and greater than or equal to (`>=`).
* **Assignment vs Equality:** A common mistake is confusing `=` with `==`. While `a = b` assigns the value of `b` to `a`, `a == b` asks the compiler whether the values are identically equal.

### **Logical Operators & Short-circuit Evaluation**
Logical operators work on boolean expressions and are the backbone of control flow (like `if/else` statements).
* **Logical AND (`&&`):** Evaluates to `true` strictly if *both* operands are `true`.
* **Logical OR (`||`):** Evaluates to `true` if *at least one* operand is `true`.
* **Short-circuit Evaluation:** This is an internal optimization behavior where Java will skip evaluating the second expression if the final outcome is already guaranteed.
    * For `&&`: If the first expression is `false`, the whole statement is guaranteed to be `false`. The second expression is skipped entirely.
    * For `||`: If the first expression is `true`, the whole statement evaluates to `true`, and the second expression is bypassed.
* **Interview Trap:** You can actually use the single bitwise operators (`&` or `|`) on boolean expressions instead of double characters. However, doing so **disables short-circuiting**, meaning both sides of the expression are forced to evaluate regardless of the first side's outcome.

### **Bitwise Operators**
Bitwise operators manipulate the raw binary values (0s and 1s) under the hood of integers.
* **Bitwise AND (`&`):** Both bits must be `1` for the result to be `1`; otherwise, it outputs `0`.
* **Bitwise OR (`|`):** If at least one bit is `1`, the result is `1`.
* **Bitwise XOR (`^`):** The output is `1` only if the bits are different (i.e., there is an odd number of `1`s).
* **Bitwise NOT (`~`):** A unary operator that flips every single bit, turning `1`s to `0`s and vice-versa.

### **Shift Operators**
Shift operators physically push bit locations to the left or right inside an integer's memory bounds.
* **Left Shift (`<<`):** Pushes all bits to the left, stuffing `0`s onto the right side. Functionally, shifting left by 1 is the equivalent of multiplying the number by 2.
    * **Edge Case:** Shifting left continuously will eventually push a `1` into the Most Significant Bit (MSB), which dictates the number's sign, abruptly turning a positive number into a large negative number.
* **Signed Right Shift (`>>`):** Pushes bits to the right. To maintain mathematical integrity, this operation checks the MSB sign bit and duplicates it (filling right-shifted spaces with `1`s if negative, `0`s if positive). This acts similarly to dividing by 2.
* **Unsigned Right Shift (`>>>`):** A "dumb" right shift that strictly injects `0`s into the empty left spaces regardless of whether the original number was positive or negative. This operator forces any negative binary number into a positive decimal translation.
* **Internal Evaluation Trap:** Shift operations are purely meant for 32-bit `int` or 64-bit `long`. Attempting to shift a `byte` or `short` causes Java to implicitly "type-promote" the variable to an `int` behind the scenes. If you try to store it back in a `byte` without explicitly typecasting `(byte)`, you will run into a compile-time error.
* **Modulo 32 Limit:** You cannot shift an integer by more than 31 times. Java applies a "Modulo 32" check on shift operations. For instance, attempting an integer left shift of `32` evaluates as `32 % 32 = 0`, essentially resulting in a shift by 0 positions.

### **Assignment Operators**
The right side of an expression is evaluated and stored into the variable declared on the left.
* **Internal Evaluation Order:** Assignments strictly run from Right-to-Left. Because of this, assigning a chain expression like `int a = b = c = 10;` is perfectly valid. The `10` is given to `c`, then `b`, and finally `a`.

### **Ternary Operator**
The ternary operator is the only operator in Java that relies on three distinct operands. It is structured as a compact `if/else` statement formatted via `condition ? trueOutput : falseOutput`.

### **Operator Precedence & Associativity**
Much like PEMDAS in standard mathematics, Java expressions rely on an operator precedence table to figure out what executes first when chained together.
* Prefix/Postfix operators evaluate first, followed by arithmetic operations, shifts, equality, logicals, and assignment at the very end.
* **Best Practice:** Do not attempt to rely on or memorize the precedence table in complex code strings. Always use parentheses `()` to construct your specific execution order. Parentheses hold the highest execution precedence and guarantee cleaner, readable code.