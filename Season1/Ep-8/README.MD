# How Google’s V8 Engine Works Behind the Scenes

JavaScript is neither a purely interpreted language nor a purely compiled one.  
It is a mix of both and is known as **JIT (Just-In-Time) compilation**, because behind the scenes, the V8 engine uses both a **compiler** and an **interpreter**.

---

## 🚀 How V8 Executes JavaScript

### 1. Parsing

When your code enters the V8 engine, **parsing happens**:

- **Lexical Analysis** → Source code is broken into **tokens** (also called _tokenization_).
- **Syntax Analysis** → Tokens are converted into an **Abstract Syntax Tree (AST)**.

---

### 2. Interpreter (Ignition)

- The AST is passed to the **Ignition Interpreter**.
- The interpreter converts the AST into **bytecode**.
- Execution begins using this bytecode.

---

### 3. Optimizing Compiler (TurboFan)

- Most code runs as bytecode.
- The portion of the code that is frequently used or can be optimized (called **hot code**) is passed to **TurboFan** (the optimizing compiler in V8).
- TurboFan converts this hot code into **optimized machine code**, enabling much faster execution.

---

### 4. De-Optimization

- TurboFan makes assumptions while compiling.  
  Example:
  - If two integers are added, TurboFan assumes they will always be integers.
  - If later you pass characters instead, the assumption fails.
  - The code is then **de-optimized** and falls back to interpretation.

⚡ This shows that **compilation and interpretation run in parallel** inside V8.

---

### 5. Garbage Collection

- V8 also manages memory using garbage collection.
- It employs several garbage collectors:
  - **Orinoco**
  - **Oilpan**
  - **Scavenger**
  - **MCompact**
- One commonly used algorithm is the **Mark-and-Sweep Algorithm**.

---

## 📝 Summary

- **JavaScript uses JIT compilation** → mix of compilation + interpretation.
- **Ignition Interpreter** → AST → Bytecode → Execution.
- **TurboFan Compiler** → Optimizes hot code → Machine code.
- **De-optimization** happens if assumptions fail.
- **Garbage Collection** runs in parallel to free memory.

---
