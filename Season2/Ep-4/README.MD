# 🚀 Express.js Routing Deep Dive

In this episode, we explored **routing in Express.js** — how to handle requests, route patterns, regex usage, and reading params.

---

## 🚦 What is Routing?

**Routing** in web development means **deciding how your server responds when a client (browser, mobile app, etc.) makes a request to a specific URL (path + method).**

👉 In short:

- **Client** → makes a request (`GET /users`)
- **Server** → uses **routes** to check _"for this URL & method, which handler should run?"_

### 🔹 Example in Express

```js
const express = require("express");
const app = express();

// Home route
app.get("/", (req, res) => {
  res.send("Welcome to Homepage 🚀");
});

// About route
app.get("/about", (req, res) => {
  res.send("About Page 📝");
});

// POST route (for submitting data)
app.post("/login", (req, res) => {
  res.send("Login Request Received ✅");
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

Here:

- `GET /` → homepage
- `GET /about` → about page
- `POST /login` → handles login

### 🔹 Types of Routing

1. **Static Routing** → Fixed URLs (`/about`, `/contact`)
2. **Dynamic Routing** → URL has variables (`/users/:id`)
   - Example: `/users/101` or `/users/102`
   - You can read `req.params.id` in Express.
3. **Query Params** → Extra info in URL (`/search?keyword=nodejs&page=2`)

## 🛣️ Route Handler (Concise)

A **route handler** is the **function that runs when a specific route is matched**. It **processes the request** and **sends a response**.

Examples:

**1. Inline (anonymous) handler**

```js
app.get("/about", (req, res) => {
  res.send("About Page");
});
```

**2. Named function**

```js
function aboutHandler(req, res) {
  res.send("About Page");
}
app.get("/about", aboutHandler);
```

**3. Multiple handlers (middleware chain)**

```js
app.get("/user", validateUser, fetchUser, (req, res) => {
  res.send(req.user);
});
```

✅ **Key points:**

- Any function that **receives** `req` and `res` and handles the request is a **route handler**.
- Can be **inline, named, or multiple in sequence**.
- Think: **Route = address**, **Route Handler = chef preparing the response 🍴**

---

## 🔹 Order of Route Handlers Matters

- Express evaluates routes **top to bottom**.
- The **first matching route wins**.

Example:

```js
app.get("/user", (req, res) => res.send("User Route"));
app.use("/user", (req, res) => res.send("Fallback User Route"));
```

👉 Here, /user will always match the first route (app.get), and the second will never run.

## 🔹 app.use() vs app.get() vs app.post()

- **app.use()** → Matches all HTTP methods (GET, POST, PUT, DELETE, etc.).
- **app.get()** → Handles only GET requests.
- **app.post()** → Handles only POST requests.

✅ **Best practice:** use app.get(), app.post(), etc. for clarity instead of a generic app.use().

## 🔹 Route Patterns in Express

Express allows pattern matching in routes using `?`, `+`, `*`, and `()` (supported in v4 & v5).

**Examples:**

### ? → Optional Character

```js
app.get("/ab?c", (req, res) => res.send("b is optional!"));
```

✅ **Matches:** /ac, /abc

### + → One or More Repetitions

```js
app.get("/ab+c", (req, res) => res.send("One or many b's allowed!"));
```

✅ **Matches:** /abc, /abbc, /abbbc

### \* → Wildcard (any characters)

```js
app.get("/ab*c", (req, res) => res.send("Anything in between allowed!"));
```

✅ **Matches:** /abc, /abXYZc, /ab123c

### () → Grouping

```js
app.get("/a(bc)?d", (req, res) => res.send("Group optional!"));
```

✅ **Matches:** /ad, /abcd

## 🔹 Regex in Routes 💡

We can use regular expressions directly in routes for advanced matching.

```js
app.get(/a/, (req, res) => res.send("Route has 'a' in it"));
// Matches: /apple, /bat, /cat

app.get(/.*fly$/, (req, res) => res.send("Ends with 'fly'"));
// Matches: /butterfly, /dragonfly
```

## 🔹 Query Params vs Dynamic Params

### 🟢 Query Params → Extra Info / Filters

- **Syntax:** ?key=value
- **Used for:** search, sorting, filtering.

```js
app.get("/products", (req, res) => {
  const { category, sort } = req.query;
  res.send(`Category: ${category}, Sort: ${sort}`);
});
```

👉 **Request:** /products?category=shoes&sort=price  
👉 **Response:** Category: shoes, Sort: price

### 🟢 Dynamic Params → Unique Resource Identity

- **Syntax:** :param
- **Used for:** fetching a specific resource.

```js
app.get("/products/:id", (req, res) => {
  res.send(`Product ID: ${req.params.id}`);
});
```

👉 **Request:** /products/123  
👉 **Response:** Product ID: 123

## 🔹 Real-World Analogy 🍴

Think of a restaurant system:

- **Customer (Client)** → Places an order (request).
- **Waiter (Server)** → Takes the order.
- **Chef (Route Handler)** → Prepares the dish (process request).
- **Waiter → Customer** → Serves the dish (response).

👉 Exactly how Express routing works!

## 🎯 Key Takeaways

- **Order matters** → first match wins.
- **Use specific methods** (GET/POST) instead of app.use().
- **Route patterns** (?, +, \*, ()) = flexible matching.
- **Regex** = advanced matching superpower.
- **Query Params** = filters / extra info.
- **Dynamic Params** = unique resource identifiers.
