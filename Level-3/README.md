# Pizza Pizza - Real-time Full-Stack Pizza Builder App

A feature-rich, high-end, real-time Pizza Builder application. Built with React (Vite), Node.js (Express), MongoDB, and WebSockets (Socket.io).

## Features

1. **Authentication**: Admin and User logins with registration, email verification, and forgot/reset password flows (via Ethereal Email test accounts).
2. **Pizza Builder**: Multi-step configuration flow (5 crust bases, 5 sauces, cheeses, veggies, meats). Checks stock availability and dynamically sums pricing.
3. **Razorpay Checkout**: Seamless test integration (runs a simulation overlay if no active Razorpay key is present in `.env`).
4. **Real-time Order Status**: Updates user screen instantly using Socket.io when the admin shifts order statuses (Order received -> In the kitchen -> Sent to delivery -> Delivered).
5. **Inventory Management**: Track and replenish stock from the Admin panel.
6. **Stock Alerts**: Automatic SMTP email dispatch to the admin when stock levels slip below 20 items.

---

## Folder Structure

```text
Level-3/
├── backend/            # Express, Node, Socket.io, Mongoose Models & Routes
│   ├── config/         # Mailer and MongoDB setups
│   ├── middleware/     # JWT authentication middlewares
│   ├── models/         # User, Order, and Inventory Schemas
│   └── routes/         # Router controllers
└── frontend/           # Vite, React, Contexts, Vanilla CSS styles
    ├── src/
    │   ├── components/ # Builder, Tracker, and Inventory cards
    │   └── context/    # Auth and Socket context definitions
    └── index.html
```

---

## Setup & Running Guide

### 1. Prerequisites
- **Node.js**: Ensure Node (version >= 18) is installed on your system.

### 2. Start the Backend Server
1. Open a terminal and navigate to the `backend/` directory:
   ```bash
   cd backend
   ```
2. Start the server (it automatically runs a local, persistent MongoDB server programmatically inside `backend/db`):
   ```bash
   npm start
   ```
   *Note: On launch, the server will output a temporary Ethereal test email account credentials. Verification and password reset links will print directly to this terminal console.*

### 3. Start the Frontend Server
1. Open a second terminal window and navigate to the `frontend/` directory:
   ```bash
   cd frontend
   ```
2. Launch the Vite development server:
   ```bash
   npm run dev
   ```
3. Open [http://localhost:5173](http://localhost:5173) in your web browser.

---

## Testing Workflow (Demonstration)

1. **Register**: Go to the registration page, enter an email (e.g. `testuser@pizza.com`), and choose a password.
2. **Verification Link**: Check the backend console output. Look for the `[Ethereal Email Preview URL]` link. Open that link in your browser and click **Verify Email** (or copy/paste the `/verify/token` url printed in logs into your address bar and press enter).
3. **Log in**: Sign in with the verified credentials.
4. **Build Pizza**: Customize your base, sauce, cheese, veggies, and meats. Observe item stock levels.
5. **Payment (Simulated)**: Click checkout. If no `.env` credentials exist, the simulated Razorpay TEST MODE modal will open. Click **Simulate Payment Success**.
6. **Admin Panel**:
   - Register or log in with the admin email (defaults to `admin@pizza.com` in `.env`).
   - Access the inventory restocker and active customer order board.
   - Click order status updates (e.g. `Kitchen`, `Delivery`) and see changes reflect on the customer screen in real time!
   - Replenish stock to see real-time updates propagate dynamically.
   - Place multiple orders to force stock levels under 20 units. Verify that a stock warning email is printed in the backend logs.
