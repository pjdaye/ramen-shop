# Getting Started – Anime Ramen Shop Ordering App

## Project Overview

We’re building an anime-inspired ramen shop ordering site that will let customers browse the menu, place orders, and receive confirmations—all while ensuring a responsive, engaging experience on both desktop and mobile browsers. The project will be developed in a single repository with the following structure:

```bash
ramen-shop/
├── backend/
├── db/
├── frontend/
└── test/
```

This document will guide GitHub Copilot (or your IDE’s assistant) with a series of prompts and commands to set up the project scaffolding and initialize the core frameworks.

---

## Step-by-Step Instructions & Commands

### 1. Repository and Directory Structure

**Goal:** Create the base repository and folder structure.

#### Instructions (Repo)

- **Create the main project folder:** `anime-ramen-shop`
- **Inside it, create subdirectories:** `backend`, `frontend`, `db`, and `test`.

#### Bash Commands (Repo)

```bash
mkdir -p anime-ramen-shop/{backend,frontend,db,test}
```

---

### 2. Setup the Frontend – React with Bootstrap

**Goal:** Scaffold a React application for the frontend and integrate Bootstrap for responsive design.

#### Instructions (Frontend)

1. **Scaffold the React App:** Use Create React App to initialize the frontend.
2. **Install Bootstrap:** Integrate Bootstrap (via npm) so that our styling is consistent.
3. **Modify the entry point to import Bootstrap CSS.**

#### Bash Commands (Frontend)

```bash
# Navigate to the frontend directory and create the React app
npx create-react-app anime-ramen-shop/frontend

# Install Bootstrap into the frontend app
npm install bootstrap --prefix anime-ramen-shop/frontend

# Append the Bootstrap import to the React app's index file
echo "import 'bootstrap/dist/css/bootstrap.min.css';" >> anime-ramen-shop/frontend/src/index.js
```

---

### 3. Setup the Backend – Node.js with Express and SQLite using Sequelize

**Goal:** Scaffold an Express API server that uses SQLite (via Sequelize) as its ORM for the MVP. This server will provide endpoints for menu retrieval, order placement, and basic admin operations.

#### Instructions (Backend)

1. **Initialize a new Node.js project** inside the `backend` folder.
2. **Install Express and Sequelize:** Configure Sequelize to use SQLite.
3. **Set up a simple Express server and a sample route (such as a health check).**

#### Bash Commands (Backend)

```bash
# Navigate to the backend folder and initialize a Node.js project
cd anime-ramen-shop/backend
npm init -y

# Install Express, Sequelize, and the SQLite3 driver
npm install express sequelize sqlite3

# Optional: Install nodemon for development
npm install --save-dev nodemon
```

#### Sample Code: `anime-ramen-shop/backend/index.js`

```javascript
const express = require('express');
const app = express();
const port = process.env.PORT || 3000;

// Middleware for JSON body parsing
app.use(express.json());

// Sample health check route
app.get('/', (req, res) => {
  res.send({ message: 'Anime Ramen Shop API is running.' });
});

// Start server
app.listen(port, () => {
  console.log(`Server is listening on port ${port}`);
});
```

Add a start script in your `package.json` (inside `/backend`):

```json
"scripts": {
  "start": "node index.js",
  "dev": "nodemon index.js"
}
```

---

### 4. Database Setup – SQLite with Sequelize

**Goal:** Set up the ORM configuration and initial models using Sequelize with SQLite to support our MVP user stories.

#### Instructions (Database)

1. **Create a configuration file** for Sequelize in a new folder (e.g., in the `/db` directory).
2. **Define models** for key entities like Menu Items and Orders.

#### Sample Code: `anime-ramen-shop/db/models.js`

```javascript
const { Sequelize, DataTypes } = require('sequelize');

// Create a Sequelize instance, pointing to a SQLite database
const sequelize = new Sequelize({
  dialect: 'sqlite',
  storage: './db/ramen-shop.sqlite'
});

// Define MenuItem model for our ramen dishes
const MenuItem = sequelize.define('MenuItem', {
  name: {
    type: DataTypes.STRING,
    allowNull: false
  },
  description: {
    type: DataTypes.TEXT
  },
  price: {
    type: DataTypes.FLOAT,
    allowNull: false
  },
  imageUrl: {
    type: DataTypes.STRING
  }
}, {
  tableName: 'menu_items'
});

// Define Order model for capturing customer orders
const Order = sequelize.define('Order', {
  customerName: {
    type: DataTypes.STRING,
    allowNull: false
  },
  customerContact: {
    type: DataTypes.STRING,
    allowNull: false
  },
  items: {
    type: DataTypes.JSON,  // Store items as JSON array
    allowNull: false
  },
  totalPrice: {
    type: DataTypes.FLOAT,
    allowNull: false
  },
  status: {
    type: DataTypes.STRING,  // e.g., "pending", "completed"
    defaultValue: "pending"
  }
}, {
  tableName: 'orders'
});

// Export the models and the sequelize instance
module.exports = { sequelize, MenuItem, Order };
```

#### Instructions for Database Initialization

Add a command in your backend startup (or a separate script) that synchronizes the database:

```javascript
// In index.js of backend (before app.listen)
const { sequelize } = require('../db/models'); // adjust path as needed

sequelize.sync({ force: false }).then(() => {
  console.log("Database & tables created!");
});
```

---

### 5. Testing & Future Expansions

**Goal:** Establish a basic testing folder for integration and unit tests.

#### Instructions (Testing)

- Place tests in the `/test` folder.
- Use frameworks such as Mocha/Chai or Jest for backend tests.
- For frontend, Create React App includes testing utilities.

#### Example Directory Tree

```bash
anime-ramen-shop/
├── backend/
│   ├── index.js
│   ├── package.json
│   └── ... (other backend files)
├── db/
│   └── models.js
├── frontend/
│   ├── package.json
│   ├── public/
│   └── src/
├── test/
│   └── sample.test.js
└── README.md
```

---

## Final Instructions Recap for GitHub Copilot

Below is a final text prompt to guide GitHub Copilot’s agent mode, outlining the steps for creating our Anime Ramen Shop ordering app:

```text
I am building an Anime Ramen Shop ordering site. It should let customers view a menu, add items to a cart, place orders, and receive confirmations. There is also a basic admin interface for managing the menu items. 

The project will be developed in a single repository named "anime-ramen-shop" with these folders:
- backend: for the Node.js/Express API server, with SQLite as the database using Sequelize.
- frontend: for a React application using Bootstrap for responsive design.
- db: for database models and configuration.
- test: for integration and unit tests.

Generate instructions in this order:
1. Create the repository with the folder structure: anime-ramen-shop/{backend,frontend,db,test}.
2. In the frontend folder, scaffold a React app using Create React App, install Bootstrap, and import the Bootstrap CSS.
3. In the backend folder, initialize a Node.js project, install Express, Sequelize, and SQLite3, and set up a basic Express server with a health check route.
4. In the db folder, create a Sequelize configuration and define models for Menu Items and Orders.
5. Provide sample code and commands for each step, including setting up start scripts, database sync, and a sample directory tree.

Let's think about this step by step.
```

---

## Running the Application

Once the scaffolding is complete:

1. **Start the backend server:**  

   ```bash
   cd anime-ramen-shop/backend
   npm run dev
   ```

2. **Start the frontend app:**  

   ```bash
   npm start --prefix anime-ramen-shop/frontend
   ```

3. Verify that the API returns a success message at `http://localhost:3000/` and the React app loads with Bootstrap styles.
