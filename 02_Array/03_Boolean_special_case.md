**The official Java documentation does not define a fixed size for a `boolean`. It is entirely up to the JDK (specifically, the JVM implementation) to decide.**

Here is a deeper look into how this works and why Java designed it this way:

### 1. What the Official Java Docs Say
According to the official Java Virtual Machine (JVM) Specification, the `boolean` data type has **no precisely defined size**. 

Unlike an `int` (which is strictly mandated to be 4 bytes everywhere) or a `long` (8 bytes), Java intentionally leaves the size of a `boolean` open-ended. It basically tells the JVM: *"Here is a true/false value. Figure out the best way to store it on the specific hardware you are running on."*

### 2. How the JDK/JVM Actually Handles It
Because Java leaves it up to the implementation, JVMs like **Oracle's HotSpot** and **OpenJDK** (which most developers use) have to make a choice. In these standard JVMs, a `boolean` is typically implemented as **1 byte (8 bits)**.

Furthermore, the JVM specification explicitly states that arrays of booleans (`boolean[]`) are encoded as arrays of bytes, meaning each element in a boolean array takes exactly 1 byte.

### 3. Why 1 Byte and Not 1 Bit?
Logically, a `boolean` only needs 1 bit of memory (`0` for false, `1` for true). So why does the JVM waste 8 bits (1 byte) to store it? 

It all comes down to **CPU Optimization**:
* Modern computer processors and RAM do not fetch data bit-by-bit. They are designed to fetch data in chunks of bytes (or words, like 4 or 8 bytes at a time). 
* If the JVM tried to pack 8 booleans into a single byte, the CPU would have to fetch the byte, and then perform extra, time-consuming bitwise operations (like shifting and masking) just to isolate the one bit you asked for.
* By dedicating a full byte to a single `boolean`, the CPU can fetch and read it instantly. Java trades a tiny amount of memory storage for a significant boost in processing speed.