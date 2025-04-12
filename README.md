# Anime Ramen Shop Ordering App

Welcome to the Anime Ramen Shop Ordering App! This repository contains the codebase for an anime-inspired online ordering system for our ramen shop. The app lets customers browse our menu, add items to a cart, place orders, and receive immediate confirmations. It also includes a basic admin interface for managing menu items and orders.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture & Repository Structure](#architecture--repository-structure)
- [Installation & Setup](#installation--setup)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Overview

The Anime Ramen Shop Ordering App is designed to provide an engaging user experience with an anime-inspired visual theme, while focusing on the core functionality required for an online ordering system. The app is built as an MVP (Minimum Viable Product) using a single repository structured into separate folders for the frontend, backend, database configuration, and tests.

## Features

- **Menu Display:** Customers can view detailed descriptions, images, and prices for our signature ramen dishes.
- **Responsive Design:** The interface is designed with Bootstrap to be fully responsive on both desktop and mobile devices.
- **Order Placement:** Users can add items to a cart and complete their orders with ease.
- **Order Confirmation:** Customers receive immediate confirmation upon order submission.
- **Admin Interface:** A basic admin panel to manage menu items (add, update, delete) and view incoming orders.

## Architecture & Repository Structure

The repository follows a modular structure to separate the concerns of frontend, backend, database configuration, and tests:

```text
anime-ramen-shop/
 ├── backend/ # Node.js + Express API server using Sequelize with SQLite
 ├── db/ # Database models and Sequelize configuration
 ├── frontend/ # React app using Create React App and Bootstrap
 └── test/ # Unit and integration tests
```

## Installation & Setup

### Prerequisites

- [Node.js](https://nodejs.org/) (v12.x or higher)
- [npm](https://www.npmjs.com/)
- Git

### Steps to Set Up the Project

1. **Clone the Repository:**

   ```bash
   git clone <repository-url>
   cd anime-ramen-shop
   ```

2. **Setup the Frontend:**

    Navigate to the frontend directory and install dependencies:

    ```bash
    cd frontend
    npm install
    ```

3. **Setup the Backend:**

    Navigate to the backend directory and install dependencies:

    ```bash
    cd ../backend
    npm install
    ```

    The backend is built with Express and uses Sequelize with SQLite. To start the server, run:

    ```bash
    npm run dev
    ```

4. **Database Initialization:**

    The Sequelize models are defined in the /db directory. When you start the backend, ensure that the database is synced. The backend startup script should include:

    ```javascript
    const { sequelize } = require('../db/models');
    sequelize.sync().then(() => {
      console.log("Database & tables created!");
    });
    ```

5. **Running Tests:**

    Tests are located in the /test directory. You can run your tests using your chosen testing framework (e.g., Jest, Mocha/Chai). For example, if using Jest:

    ```bash
    npm test
    ```

## Usage

- **Frontend:**

    The React app is served on the default port (usually <http://localhost:3000>). This is where customers can view the menu, add items to the cart, and place orders.

- **Backend API:**

    The Express server runs on port 3000 (or your designated port) and provides RESTful endpoints for:

  - Retrieving the menu: GET /menu
  - Placing orders: POST /orders
  - Administrative functions: POST /admin/menu, PUT /admin/menu/:id, DELETE /admin/menu/:id

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature or bugfix (git checkout -b feature/your-feature-name).
3. Commit your changes (git commit -am 'Add your feature').
4. Push to the branch (git push origin feature/your-feature-name).
5. Open a Pull Request.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
