# Deep Dive into Libuv

In this lecture, we are going to **deep dive into Libuv** — what it does and how it works.

---

## All the non-blocking I/O and asynchronous tasks in Node.js are handled by Libuv. Internally, Libuv uses the event loop, thread pool, and callback queue.

---

## 🔑 Libuv Has 3 Main Parts

1. **Event Loop** → Checks whether the call stack is empty or not.
2. **Thread Pool** → Handles heavy operations (like file I/O, DNS, crypto).
3. **Callback Queue** → Stores callbacks that are ready to be executed.

---

## 🌀 Event Loop in Detail

- The **Event Loop** is the heart of Node.js async execution.
- It has **4 major phases**, and before each phase, a **priority cycle (microtask queue)** is executed.
- Each phase has its **own queue of callbacks**.

### ⚡ How the Event Loop Works

1. **Priority Cycle (Microtasks)**

   - Runs before every phase.
   - Executes `process.nextTick()` first.
   - Then executes **promise callbacks** (resolved/rejected promises).

2. **Timer Phase**

   - Executes callbacks scheduled by `setTimeout()` and `setInterval()`.

3. **Poll Phase**

   - Fetches new I/O events (like file read/write, network).
   - Executes I/O-related callbacks.
   - In **Node.js**, if there is nothing left to do, the event loop **waits in the poll phase** (unlike browsers, where it keeps running).

4. **Check Phase**

   - Executes callbacks scheduled by `setImmediate()`.

5. **Close Callbacks Phase**
   - Executes callbacks when a resource (like socket/handle/stream) is closed.
   - Example:
     ```js
     socket.on("close", () => {
       console.log("Socket closed");
     });
     ```

👉 After each phase, the event loop goes back to the **priority cycle (blue circle)** to check microtasks again.

---

## 🖼️ Notes from Diagrams

- **Event Loop (Browser vs Node.js)**

  - In **browsers**, the event loop keeps running continuously.
  - In **Node.js**, when there is nothing left, the event loop **waits in the poll phase**. (See _9th image in assets folder_).

- **File Reading vs Other Async Ops**

  - Reading a file takes more time compared to other async operations (like timers or immediate callbacks), because it is offloaded to the **Thread Pool**.

- **Queue Rules**
  - The event loop will move to the **next phase only when the current phase’s queue is completely empty**.

---

## 📝 Summary

- Libuv powers Node.js async execution with **Event Loop + Thread Pool + Callback Queue**.
- **Event Loop** cycles through phases, but always runs **microtasks (priority cycle)** first.
- Node.js differs from browsers: it **waits in poll phase** when idle.
- Heavy tasks (file I/O, crypto) use the **Thread Pool**.

---
