# 🔐 User Authentication Flow

This guide explains the basic steps for handling **user sign-up and login** securely in a Node.js + Express backend.

## ✨ Steps to Store User Data (Sign Up)

### 1. **Validate User Data**

- Never trust `req.body` directly.
- Create a helper function for validation.
- Example: put your validation logic inside a `utils/validation.js` file.

### 2. **Encrypt the Password**

- Install **bcrypt**:

```bash
npm install bcrypt
```

- Hash the password using:

```javascript
const bcrypt = require("bcrypt");
const hashedPassword = await bcrypt.hash(password, 10);
```

### 3. **Save User in Database**

- Store the encrypted password instead of plain text.
- Example:

```javascript
const user = new User({ ...req.body, password: hashedPassword });
await user.save();
```

## 🔑 Login API Steps

### 1. **Validate Data**

- Check if `email` and `password` are provided.

### 2. **Find User by Email**

- Example:

```javascript
const user = await User.findOne({ email });
if (!user) throw new Error("Invalid email or password");
```

### 3. **Compare Passwords**

- Use bcrypt's `compare` function:

```javascript
const isMatch = await bcrypt.compare(password, user.password);
if (!isMatch) throw new Error("Invalid email or password");
```

### 4. **Return Response**

- On success, send user data (excluding password).
- Optionally, generate a token (JWT) for authentication.

## 📂 Project Structure (Example)

```
project/
├── models/
│   └── User.js
├── routes/
│   └── auth.js
├── utils/
│   └── validation.js
├── server.js
```

## ✅ Important Notes

- Always validate and sanitize data before saving.
- Never store plain text passwords.
- Use POST for login/signup requests.
