## ID: 22059  
## Names: Rusimbi Patrick  
--- 
### Q1) What is a stack, and how does a process use it during execution?

**Answer:**
A **stack** is a region of memory used for managing function calls, local variables, and control flow during program execution. It operates on a **Last-In-First-Out (LIFO)** principle, meaning the last item added to the stack is the first one to be removed.

**How a process uses the stack:**
1. **Function Calls:** When a function is called, the return address (where to resume after the function completes) and parameters are pushed onto the stack.
2. **Local Variables:** Space for local variables is allocated on the stack.
3. **Control Flow:** The stack keeps track of nested function calls, allowing the program to return to the correct location after a function finishes.
4. **Stack Frames:** Each function call creates a **stack frame**, which contains its local variables, parameters, and return address. When the function exits, its stack frame is popped off the stack.

The stack is crucial for managing the execution context of a program.

---

### Q2) Is there any difference between `String[] args` and `String args[]` in Java?

**Answer:**
No, there is **no functional difference** between `String[] args` and `String args[]` in Java. Both are valid ways to declare an array of strings, and they behave identically.

- `String[] args` is the preferred style because it clearly indicates that `args` is an array of `String` objects.
- `String args[]` is an alternative syntax inherited from C/C++ but is less commonly used in Java.

Example:
```java
public static void main(String[] args) { ... }  // Preferred
public static void main(String args[]) { ... }  // Also valid
```

---

### Q3) At what time can you use `nextLine()` or `next()`?

**Answer:**
`nextLine()` and `next()` are methods provided by the `Scanner` class in Java for reading input from the user or a file.

- **`next()`**: Reads the next token (a single word) from the input. It stops reading at whitespace (e.g., space, tab, or newline).
  ```java
  Scanner scanner = new Scanner(System.in);
  String word = scanner.next(); // Reads a single word
  ```

- **`nextLine()`**: Reads the entire line of input, including spaces, up to the newline character (`\n`).
  ```java
  Scanner scanner = new Scanner(System.in);
  String line = scanner.nextLine(); // Reads an entire line
  ```

**When to use:**
- Use `next()` when you want to read individual tokens (e.g., words).
- Use `nextLine()` when you want to read an entire line of text, including spaces.

**Note:** Be cautious when mixing `next()` and `nextLine()` because `next()` does not consume the newline character, which can cause unexpected behavior if `nextLine()` is called afterward.

---

### Q4) Between `boolean condition = true` and `boolean condition = Boolean.TRUE;`, which one is the best to use?

**Answer:**
- **`boolean condition = true;`** is the best and most common way to assign a boolean value. It uses the primitive `boolean` type, which is more efficient in terms of memory and performance.
- **`boolean condition = Boolean.TRUE;`** uses the `Boolean` wrapper class, which is an object representation of the primitive `boolean`. This is less efficient and unnecessary for simple boolean assignments.

**Best Practice:**
Use `boolean condition = true;` for simplicity and efficiency unless you specifically need the `Boolean` object for some reason (e.g., working with collections that require objects).

---

### Q5) How many possible status codes can we use in `System.exit()`?

**Answer:**
The `System.exit(int status)` method in Java accepts an integer status code as an argument. The status code can be any integer value, but by convention:
- **`0`**: Indicates successful termination.
- **Non-zero values (e.g., `1`, `-1`)**: Indicate abnormal termination or specific error conditions.

**Number of Possible Status Codes:**
Since the status code is an `int`, there are **2³² (4,294,967,296)** possible values, ranging from `-2,147,483,648` to `2,147,483,647`. However, only a small subset of these values is typically used in practice.

**Example:**
```java
System.exit(0);  // Successful termination
System.exit(1);  // Indicates an error
```
