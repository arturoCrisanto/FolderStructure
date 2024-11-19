# Folder Structure

1. Initialize a Project:

- Create a folder named using your surname (e.g., Smith_API_Project).
- Initialize a Node.js project

```bash
npm init -y
```

2. Install Required Dependencies:

```bash
npm i express nodemon dotenv
```

3. Update `package.json` Scripts:

Add the following `scripts` to run the server easily

```bash
"dev": "nodemon index.js"
```

4 Create Essential Files:

.`env`: To store environment variables.
.`gitignore`: To exclude sensitive and unnecessary files like `.env` and `node_modules`.

## Folder and File Structure

Your project should look like this:

```bash
Smith_API_Project/
├── node_modules/
├── controllers/
│   └── itemController.js
├── models/
│   └── itemModel.js
├── routes/
│   └── itemRoutes.js
├── .env
├── .gitignore
├── index.js
├── package.json
└── package-lock.json
```

## Step-by-Step Implementation

1. Create the .env File
   In the .env file, set the server's port:

```bash
PORT=3000
```

2. Create the .gitignore File
   In the .gitignore file, exclude sensitive files:

```bash
node_modules
.env
```

3. Create the Model
   The model handles data. In models/itemModel.js:

```javascript
// models/itemModel.js
let items = [
  { id: 1, name: "Product A", price: 10 },
  { id: 2, name: "Product B", price: 20 },
  { id: 3, name: "Product C", price: 30 },
];

module.exports = items;
```

4. Create the Controller
   The controller contains the logic for each endpoint. In controllers/itemController.js:

```javascript
// controllers/itemController.js
const items = require("../models/itemModel");

// Get all items
const getAllItems = async (req, res) => {
  try {
    res
      .status(200)
      .json({ message: "Items retrieved successfully", data: items });
  } catch (error) {
    res
      .status(500)
      .json({ message: "An error occurred", error: error.message });
  }
};

// Get a specific item by ID
const getItemById = async (req, res) => {
  try {
    const id = parseInt(req.params.id);
    const item = items.find((item) => item.id === id);
    if (item) {
      res
        .status(200)
        .json({ message: "Item retrieved successfully", data: item });
    } else {
      res.status(404).json({ message: "Item not found" });
    }
  } catch (error) {
    res
      .status(500)
      .json({ message: "An error occurred", error: error.message });
  }
};

// Add a new item
const addItem = async (req, res) => {
  try {
    const newItem = req.body;
    items.push(newItem);
    res.status(201).json({ message: "Item added successfully", data: items });
  } catch (error) {
    res
      .status(500)
      .json({ message: "An error occurred", error: error.message });
  }
};

// Update an existing item
const updateItem = async (req, res) => {
  try {
    const id = parseInt(req.params.id);
    const index = items.findIndex((item) => item.id === id);
    if (index !== -1) {
      items[index] = { ...items[index], ...req.body };
      res
        .status(200)
        .json({ message: "Item updated successfully", data: items });
    } else {
      res.status(404).json({ message: "Item not found" });
    }
  } catch (error) {
    res
      .status(500)
      .json({ message: "An error occurred", error: error.message });
  }
};

// Delete an item
const deleteItem = async (req, res) => {
  try {
    const id = parseInt(req.params.id);
    const index = items.findIndex((item) => item.id === id);
    if (index !== -1) {
      items.splice(index, 1);
      res
        .status(200)
        .json({ message: "Item deleted successfully", data: items });
    } else {
      res.status(404).json({ message: "Item not found" });
    }
  } catch (error) {
    res
      .status(500)
      .json({ message: "An error occurred", error: error.message });
  }
};

module.exports = {
  getAllItems,
  getItemById,
  addItem,
  updateItem,
  deleteItem,
};
```

5. Create the Routes
   The routes define the endpoints and link them to the controller. In routes/itemRoutes.js:

```javascript
// routes/itemRoutes.js
const express = require("express");
const router = express.Router();
const {
  getAllItems,
  getItemById,
  addItem,
  updateItem,
  deleteItem,
} = require("../controllers/itemController");

// Route definitions
router.get("/", getAllItems);
router.get("/:id", getItemById);
router.post("/", addItem);
router.put("/:id", updateItem);
router.delete("/:id", deleteItem);

module.exports = router;
```

6. Connect Everything in server.js
   In the server.js file:

```javascript
// index.js
require("dotenv").config();
const express = require("express");
const app = express();
const PORT = process.env.PORT;

// Middleware
app.use(express.json());

// Routes
const itemRoutes = require("./routes/itemRoutes");
app.use("/items", itemRoutes);

// Start server
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```

# Run and Test

1. Start the server using nodemon:

```bash
npm run dev
```

2. Test the endpoints using Postman or curl:

GET `/items` - Retrieve all items
GET `/items/:id` - Retrieve a specific item
POST `/items` - Add a new item
PUT `/items/:id` - Update an item
DELETE `/items/:id` - Remove an item
