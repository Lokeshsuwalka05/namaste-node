# 📘 Backend Schema & API Validation Guide

Validation and sanitization are the backbone of any secure backend.
**Never trust req.body** — agar tu har field properly validate nahi karega to koi bhi hacker teri API ko crash ya exploit kar sakta hai.

## 🔑 Why Validation Matters?

- **Protects your DB** from invalid / malicious data
- **Prevents app crashes** (e.g., huge strings in names, wrong types, etc.)
- **Improves data consistency & integrity**
- **Ensures security** (no injections, no garbage data)

## 🏗 Schema Level Validation (Mongoose)

### 1. Schema Types Options

Mongoose schema me bahut saare options hote hain:

- **required** → field must be present
- **unique** → prevent duplicates (DB index)
- **lowercase** → auto converts string to lowercase
- **trim** → removes extra spaces
- **minLength / maxLength** → control string length
- **min / max** → control number range
- **default** → fallback value if nothing is provided

### 2. Example User Schema

```javascript
const validator = require("validator");
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema(
  {
    firstName: {
      type: String,
      required: true,
      trim: true,
      minLength: 2,
      maxLength: 30,
    },
    lastName: {
      type: String,
      trim: true,
      minLength: 2,
      maxLength: 30,
    },
    emailId: {
      type: String,
      required: true,
      unique: true,
      lowercase: true,
      trim: true,
      validate: [
        {
          validator: (value) => validator.isEmail(value),
          message: "Invalid email format",
        },
      ],
    },
    password: {
      type: String,
      required: true,
      validate: {
        validator: (value) =>
          validator.isStrongPassword(value, {
            minLength: 8,
            minNumbers: 1,
            minUppercase: 1,
            minSymbols: 1,
          }),
        message: "Password must be strong",
      },
    },
    age: {
      type: Number,
      min: 18,
    },
    gender: {
      type: String,
      enum: ["male", "female", "others"],
      validate: {
        validator: (val) => ["male", "female", "others"].includes(val),
        message: "Invalid gender value",
      },
    },
    about: {
      type: String,
      default: "I will learn JavaScript for sure",
      trim: true,
    },
    skills: {
      type: [String],
      validate: {
        validator: (arr) => arr.length <= 10,
        message: "Skills cannot be more than 10",
      },
      default: [],
    },
    photoUrl: {
      type: String,
      default: "https://default-photo-url.com",
      validate: {
        validator: (value) => validator.isURL(value),
        message: "Invalid photo URL",
      },
    },
  },
  { timestamps: true }
);
```

**👉 Note:** `timestamps: true` → automatically adds createdAt and updatedAt.

## 🛡 API Level Validation

**Schema validation alone is not enough** ⚠️
**Hamesha API pe bhi validation karo** because:

- **req.body can contain extra fields**
- **Hackers can bypass frontend validations**

### Example: Patch Request Validation

```javascript
app.patch("/user/:userId", async (req, res) => {
  try {
    const allowedFields = [
      "firstName",
      "lastName",
      "age",
      "gender",
      "about",
      "skills",
      "photoUrl",
    ];
    const updates = Object.keys(req.body);

    // Block invalid updates
    const isValid = updates.every((field) => allowedFields.includes(field));
    if (!isValid) {
      return res.status(400).send("Invalid update fields");
    }

    // Skills limit check
    if (req.body.skills && req.body.skills.length > 10) {
      return res.status(400).send("Skills cannot be more than 10");
    }

    const user = await User.findByIdAndUpdate(req.params.userId, req.body, {
      new: true,
      runValidators: true,
    });

    if (!user) return res.status(404).send("User not found");

    res.send("Update successful");
  } catch (err) {
    res.status(400).send("Something went wrong: " + err.message);
  }
});
```

## 🔍 DB Level Validation vs API Level Validation

| Validation Level | Purpose                                                     |
| ---------------- | ----------------------------------------------------------- |
| Schema (DB)      | Data integrity & consistency at database level              |
| API              | Security, request sanitization, preventing malicious fields |

**👉 Always use both together for max safety.**

## 🧼 Data Sanitization

**Before saving any data into DB:**

- **trim** → remove spaces
- **lowercase** → normalize case
- **validator library** → validate email, password, URL
- **Escape dangerous characters** (for XSS) if storing text

## 🔗 JSON vs JavaScript Object

### JS Object:

- In-memory structure (`{ name: "Lokesh" }`)
- Keys can be functions, symbols, variables
- Flexible but not strict

### JSON Object:

- Strict text format (`'{"name":"Lokesh"}'`)
- Keys must be strings
- Values limited to string, number, boolean, null, array, object
- Used for data transfer (API requests, DB storage)

**👉** Every JSON object can be parsed into a JS object, but not every JS object can be converted to JSON (functions, undefined, etc. not allowed).

## 🛠 Tools

- **Mongoose** → Schema-level validation
- **Validator.js** → Strong validators (email, password, URL)
- **API Middleware** → Extra safety (e.g., Joi, express-validator)

## 🚀 Key Takeaways

- **Never trust req.body** → always validate & sanitize
- **Use Schema + API level validation** (both together)
- **Use validator.js** for strong field validation
- **Apply default values** for fallback
- **Enable runValidators: true** on update queries
- **Always keep DB safe** from malicious input
