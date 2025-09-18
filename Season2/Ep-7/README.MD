# 🚀 Mongoose & API Deep Dive

In this episode, we explored **building APIs with Express.js and Mongoose** and handling data in MongoDB.

## 1️⃣ Always Connect Database Before Starting the Server

```javascript
mongoose.connect(DB_URL).then(() => {
  app.listen(PORT, () => console.log("Server running..."));
});
```

**Why?**

- If your server starts **before the DB connection**, requests may fail.
- You might get errors like: `Cannot read property 'find' of undefined`.
- Data operations could crash the app or leave inconsistent results.

## 2️⃣ Mongoose Schema & Model

- **Schema** → Defines the structure of a document: fields like `firstName`, `lastName`, `email`.
- **Model** → A wrapper around the schema to perform CRUD operations.

```javascript
const userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String,
  email: { type: String, unique: true },
});

const User = mongoose.model("User", userSchema);
```

## 3️⃣ Create a User (POST /signup)

```javascript
app.post("/signup", async (req, res) => {
  const user = new User(req.body);
  await user.save();
  res.send("User added successfully!");
});
```

**Flow:** `Schema → Model → Instance → Save to DB`

## 4️⃣ Sending Data via API / Postman

- Postman sends **JSON**, but Express cannot read JSON directly.
- Use middleware:

```javascript
app.use(express.json());
```

- Now your API can **dynamically receive user data**.

## 5️⃣ `findOne()` Clarification

- `User.findOne({ email: "abc@gmail.com" })` returns **the first matching document in natural DB order**.
- **Natural order** = the order documents are stored in MongoDB (usually insertion order).
- ❌ It doesn't automatically return the oldest unless you sort by a timestamp.

```javascript
// Oldest user
await User.findOne({ email: "abc@gmail.com" }).sort({ createdAt: 1 });

// Newest user
await User.findOne({ email: "abc@gmail.com" }).sort({ createdAt: -1 });
```

💡 **Masala:** Always think: `findOne()` = "first match as MongoDB sees it," not oldest/newest.

## 6️⃣ Other APIs

- **Get user by email** → `GET /user?email=abc@gmail.com`
- **Feed API** → `GET /feed` → Returns all users.
- **Delete user** → `DELETE /user/:id`
- **Update user** → `PATCH /user/:id` (partial update)

**PATCH vs PUT:**

- **PATCH** → Update specific fields.
- **PUT** → Replace the entire document.

## 7️⃣ Pro Tips / Masala

- Always **handle errors**: use try-catch or `.catch()`.
- Apply **unique indexes** for fields like `email` to avoid duplicates.
- Explore **Mongoose model methods** for powerful queries: `findById`, `updateOne`, `deleteOne`.
- Use **Postman / Thunder Client** for testing APIs before frontend integration.

## 8️⃣ Summary

- Connect DB **before server**.
- Schema → Model → Instance → Save workflow.
- `express.json()` middleware is mandatory for reading JSON.
- `findOne()` returns **first match in natural order**, use `.sort()` if needed.
- Build **dynamic APIs**: POST, GET, PATCH, DELETE.

**Remember:** MongoDB + Mongoose = 🚀 fast, flexible, and scalable backend magic!
