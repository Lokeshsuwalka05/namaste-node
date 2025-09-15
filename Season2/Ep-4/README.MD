# 🚀 Express.js Routing Deep Dive

In this episode, we explored **routing in Express.js** — how to handle requests, route patterns, regex usage, and reading params.

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
