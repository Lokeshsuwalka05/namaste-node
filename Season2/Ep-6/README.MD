# 📘 MongoDB + Mongoose + Express Setup

This guide explains how to **connect MongoDB with Node.js (Express)** using **Mongoose**, and create a simple **signup API**.

## 🔌 Why Always Use Mongoose?

- Mongoose is an **ODM (Object Data Modeling) library** for MongoDB.
- It gives you a **structured way** to define schema and interact with the database.
- Provides validation, middlewares, and a clean syntax compared to raw MongoDB driver.

## ⚠️ Connect DB Before Starting Server

👉 **Rule:** Always connect your database **first**, then start listening to the server.

❌ Problem if you don't:

- If DB is not connected and server is already running:
  - API requests (like `/signup`) will fail.
  - You may get errors like `MongoNotConnectedError`.
  - Users won't be able to store/fetch data.
  - Basically → server chal raha hai but data ka gate hi closed hai 🚪.

## 🏗️ Schema & Model

- **Schema** → Blueprint (what fields you want in your document).
- **Model** → Constructor based on schema, used to interact with DB.

Example:

```javascript
const mongoose = require("mongoose");

// User Schema
const userSchema = new mongoose.Schema({
  firstName: { type: String, required: true },
  lastName: String,
  emailId: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  age: Number,
});

// User Model
const User = mongoose.model("User", userSchema);

module.exports = { User };
```

## 🚀 Creating Express Server + MongoDB Connection

```javascript
const express = require("express");
const mongoose = require("mongoose");
const { User } = require("./models/user");

const app = express();
app.use(express.json()); // Middleware for JSON parsing

// DB Connection
mongoose
  .connect("mongodb://localhost:27017/mydb")
  .then(() => {
    console.log("✅ Database Connected");
    app.listen(3000, () => {
      console.log("🚀 Server is running on port 3000");
    });
  })
  .catch((err) => {
    console.error("❌ DB Connection Failed:", err);
  });
```

## ✨ Signup API (POST /signup)

```javascript
app.post("/signup", async (req, res) => {
  try {
    const { firstName, lastName, emailId, password, age } = req.body;

    // Create instance of User model
    const user = new User({ firstName, lastName, emailId, password, age });

    // Save to DB
    await user.save();

    res.status(201).send("🎉 User Registered Successfully!");
  } catch (err) {
    console.error(err);
    res.status(500).send("❌ Something went wrong");
  }
});
```

## 📬 Testing with Postman

1. Run your server.
2. Open Postman → `POST http://localhost:3000/signup`.
3. Send JSON body:

```json
{
  "firstName": "Maya",
  "lastName": "Sharma",
  "emailId": "maya@gmail.com",
  "password": "123",
  "age": 25
}
```

4. ✅ Check MongoDB, document will be inserted.

## 🛠️ Flow of Adding a User

`UserSchema → UserModel → Create Instance → Save to DB`

Think of it like 👇

- **Schema** = Form design 📝
- **Model** = Printing that form 📄
- **Instance** = Filling the form ✍️
- **Save()** = Submitting form to office 📂
