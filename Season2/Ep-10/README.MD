# 🔐 Advanced Authentication in Node.js (JWT + Cookies)

Authentication is the **backbone of secure applications**. In this section, we explore how to implement **JWT-based authentication** with **cookies** in Node.js.

## 🔹 Flow of Login Authentication

1. **Client sends login request** → with email & password.
2. **Server validates credentials** → checks if email & password are correct.
3. **If valid** → server creates a **JWT (JSON Web Token)**.
4. **Token is sent back to client** inside a **cookie**.
5. **Next requests** → client automatically sends the cookie back.
6. **Server verifies token** → extracts user info (like `_id`) → fetches user data from DB.

👉 Result: **Stateless authentication** (no session storage needed on the server).

## 🔹 What is a Cookie?

- A **cookie** is a small piece of data stored in the browser.
- It is sent automatically with every request to the same server.
- Perfect place to store the JWT (instead of localStorage/sessionStorage).

## 🔹 What is JWT?

**JWT (JSON Web Token)** has 3 parts:

1. **Header** → algorithm & token type.
2. **Payload** → actual data (e.g., user `_id`, email).
3. **Signature** → verifies token integrity.

Example:

```
xxxxx.yyyyy.zzzzz
```

- `xxxxx` → Header (Base64 encoded)
- `yyyyy` → Payload (Base64 encoded)
- `zzzzz` → Signature (HMAC/secret-based)

## 🔹 Creating & Validating a JWT

```javascript
const jwt = require("jsonwebtoken");
const secretKey = "MY_SECRET_KEY";

// ✅ Creating a token
const token = jwt.sign({ _id: user._id }, secretKey, { expiresIn: "1h" });

// ✅ Verifying a token
try {
  const decoded = jwt.verify(token, secretKey);
  console.log(decoded._id); // user id
} catch (err) {
  console.error("Invalid Token", err);
}
```

- **Creating** → `jwt.sign(payload, secretKey)`
- **Validating** → `jwt.verify(token, secretKey)`
- **Decoding** (without verifying) → `jwt.decode(token)`

## 🔹 Real-World Example Flow

- User logs in → JWT created with `{ _id }` in payload.
- JWT stored inside cookie.
- Next API call: `/profile`
  - Server extracts token from cookie.
  - Runs `jwt.verify(token, secretKey)`.
  - Decoded payload gives `_id`.
  - Server fetches user details from DB & sends back to client.

💡 Masala: This is why you don't need to keep session data in memory — JWT makes your app **scalable** and **stateless**.

## 🔹 Schema Methods vs Schema Statics (Mongoose)

- **Schema Methods** → Work on a single document (instance level). Example: `user.generateAuthToken()`

```javascript
userSchema.methods.generateAuthToken = function () {
  return jwt.sign({ _id: this._id }, secretKey);
};
```

- **Schema Statics** → Work on the entire model (class level). Example: `User.findByCredentials(email, password)`

```javascript
userSchema.statics.findByCredentials = async function (email, password) {
  return await this.findOne({ email });
};
```

💡 Masala:

- **Methods** = "behavior of an object" (per user).
- **Statics** = "utility of a class" (on whole collection).

## 🔹 Best Practices

- Always store **minimal data** in JWT (usually `_id` only).
- Use `httpOnly` cookies → prevent client-side JS access (protect against XSS).
- Always set `expiresIn` for tokens.
- Never store **sensitive data** (like password) inside JWT payload.

## ✅ Summary

- Cookies + JWT = secure, stateless authentication.
- `jwt.sign()` → create token.
- `jwt.verify()` → validate token.
- **Schema methods/statics** in Mongoose → make code cleaner & reusable.
