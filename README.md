# **Registration Form**  

A simple **registration system** built with **HTML, CSS, Node.js (Express.js), and MongoDB** to **store user information securely**.

---

## **Overview**  
This project allows users to **sign up** by entering their details, which are then stored in a **MongoDB database**. It includes **form validation**, **password hashing**, and **error handling** to ensure **data security and integrity**.

### **Features**  
✔️ **User Registration** (Name, Email, Password, etc.)  
✔️ **Form Validation** (Client & Server-side)  
✔️ **Secure Password Storage** (bcrypt.js)  
✔️ **MongoDB Integration** (Mongoose)  
✔️ **Express.js for Backend API**  

---

## **Tech Stack**  
- 🌐 **Frontend:** HTML, CSS  
- 🖥️ **Backend:** Node.js, Express.js  
- 🛢️ **Database:** MongoDB (Mongoose ORM)  
- 🔐 **Security:** bcrypt.js for password hashing  

---

## **Installation & Setup**  

### **1️⃣ Clone the Repository**  
```bash
git clone https://github.com/your-username/registration-form-node-mongodb.git
cd registration-form-node-mongodb
```

### **2️⃣ Install Dependencies**  
```bash
npm install
```

### **3️⃣ Set Up MongoDB**  
Ensure you have **MongoDB installed** or use **MongoDB Atlas**.  
Create a **`.env` file** and add your **MongoDB connection string**:  
```
MONGO_URI=mongodb://localhost:27017/userdb
PORT=3000
```

### **4️⃣ Start the Server**  
```bash
node server.js
```
- Open **`http://localhost:3000`** in your browser.

---

## **File Structure**  
```
/registration-form
  ├── /public       # Frontend (HTML, CSS)
  ├── /views        # EJS Templates (if using templating)
  ├── /routes       # Express Routes
  ├── /models       # Mongoose Models
  ├── server.js     # Main Server File
  ├── .env          # Environment Variables
  ├── package.json  # Project Dependencies
```

---

## **API Endpoints**  

| Method | Endpoint      | Description       |
|--------|-------------|------------------|
| POST   | `/register`  | Register a new user |
| GET    | `/users`     | Fetch all users  |

---

## **Code Snippets**  

### **User Model (`models/User.js`)**
```javascript
const mongoose = require("mongoose");
const bcrypt = require("bcrypt");

const userSchema = new mongoose.Schema({
  name: String,
  email: { type: String, unique: true },
  password: String
});

// Hash password before saving
userSchema.pre("save", async function (next) {
  if (!this.isModified("password")) return next();
  this.password = await bcrypt.hash(this.password, 10);
  next();
});

module.exports = mongoose.model("User", userSchema);
```

### **Server Setup (`server.js`)**
```javascript
const express = require("express");
const mongoose = require("mongoose");
const dotenv = require("dotenv");
const User = require("./models/User");

dotenv.config();
const app = express();
app.use(express.json());

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log("MongoDB Connected"));

app.post("/register", async (req, res) => {
  try {
    const user = new User(req.body);
    await user.save();
    res.status(201).send("User Registered");
  } catch (error) {
    res.status(400).send(error.message);
  }
});

app.listen(process.env.PORT, () => console.log(`Server running on port ${process.env.PORT}`));
```

---

## **Future Enhancements 🚀**
🔹 Add **Login & Authentication** (JWT)  
🔹 Implement **User Profile Dashboard**  
🔹 Improve UI with **Bootstrap/Tailwind CSS**  
🔹 Deploy on **Heroku/Vercel**  

---

## **Contributors**  
👤 **Your Name** - [GitHub Profile](https://github.com/Bishaljay)  
