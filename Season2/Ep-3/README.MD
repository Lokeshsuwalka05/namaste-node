# 🚀 Express Server Basics

In this episode, we created our **first Express server**.

---

## Why Express? 🤔

- Yes, we can create a server using Node’s built-in `http` module.
- But… most companies prefer **Express.js** because:
  - Less boilerplate, more productivity ⚡
  - Easy routing & middleware support
  - Widely used in production apps

👉 That’s why we’re building with Express.

---

## Nodemon 🔄 (Auto-Refresh for Developers)

Normally:

- With `node index.js`, you must restart the server **manually** after every change.

With **Nodemon**:

- It **auto-restarts** the server when you save changes.
- Saves time ⏳, saves effort 💡.

👉 Install globally:

```bash
npm install -g nodemon
```

👉 Run your project with:

```bash
nodemon index.js
```

## What does -g mean in npm install? 🌍

- -g → Global installation.
- Package is available everywhere, not just in one project.
- Example: installing nodemon globally makes sense because you’ll use it in multiple projects.

## Request Handler ⚡

### Every server needs something to handle incoming requests.

- Request comes in → Handler processes it → Response goes out

### Restaurant Analogy 🍴

- Customer (client) → order deta hai (request).
- Waiter (server) → order receive karta hai.
- Chef (request handler) → order process karke khana banata hai.
- Waiter → khana customer ko deliver karta hai (response).

## Dependencies 📦

- Dependencies are the packages your project depends on to work.

### Example:

- express → for server setup
- nodemon → (dev dependency) for auto-restart
- Without them → project won’t run properly.

## Quick Demo Code 👨‍💻

```bash
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Hello from Express server 🚀");
});

app.listen(3000, () => {
  console.log("✅ Server is running on port 3000...");
});
```

## Key Takeaways 🎯

- Express simplifies server creation.
- Nodemon boosts development speed.
- Understand the client → server → handler → response flow.
- Always keep track of your dependencies.
