🍽️ Crave: Premium Indian Takeaway Platform

Crave is a modern, high-performance web application designed for the high-throughput environment of a premium takeaway food service. It focuses on speed, operational automation (Kitchen Display System), and a delightful user experience.

✨ Core Features & Innovations

Crave is built around several unique, production-grade features:

Atomic Daily Order Numbering: Customers receive a short, memorable order ID (e.g., #045) that resets daily. The system uses MongoDB transactions to guarantee zero duplicate numbers under high concurrency.

Smart Loyalty Engine (Crave Coins): Rewards system allowing customers to earn points (1 coin per ₹10 spent) and redeem them for up to 50% off their next order.

Role-Based Access Control (RBAC): Strict security ensuring Customer, CounterStaff, KitchenManager, and SuperAdmin each have access only to necessary APIs (e.g., only staff can update order status).

Live Kitchen Display System (KDS): Staff dashboard that provides a Kanban-style view of the queue (Paid → Preparing → Ready). Updates are pushed in real-time via WebSockets (Socket.io).

Intelligent Pickup Time: Orders are assigned an estimated pickup time dynamically calculated based on the current volume of orders in the "Preparing" status (Kitchen Load Algorithm).

Secure Payments: Uses Stripe for payments with full INR compliance (handling cross-border data requirements for Indian regulations).

💻 Tech Stack

This project is implemented as a microservices-style architecture split into two repositories. 

Layer

Technology

Key Libraries

Frontend (Client)

React (Vite)

Redux Toolkit (State), Tailwind CSS (Theming), Framer Motion (Animations), Stripe.js, Axios

Backend (API)

Node.js, Express.js

Mongoose (MongoDB ODM), JSON Web Tokens (JWT), Bcrypt, Stripe API, Socket.io, Nodemailer

Database

MongoDB

Highly scalable NoSQL database for flexible schemas.

Deployment

Vercel (Frontend), Render (Backend)

Cross-domain cookie handling (SameSite: None), HTTPS enforced.

🚀 Setup & Installation

1. Backend (crave-backend)

The backend requires Node.js, MongoDB Atlas, and external API keys.

Clone the Repository:

git clone [BACKEND_REPO_URL] crave-backend
cd crave-backend
npm install


Create .env File: Populate the environment variables.

NODE_ENV=development
MONGO_URI=mongodb+srv://... (Your Atlas URI)
JWT_SECRET=YOUR_RANDOM_SECRET
STRIPE_SECRET_KEY=sk_test_...
CLIENT_URL=http://localhost:5173
# SMTP details required for email confirmations
SMTP_USER=...
SMTP_PASS=...


Seed the Database (Initial Setup):
Run the seeder to populate the menu and create admin users.

# Wipe old data and insert 200+ Indian dishes
node src/seeder.js
# Create Staff Accounts (Chef/Admin)
node src/createStaff.js


Run the Server:

npm run dev


2. Frontend (crave-frontend)

The frontend application serves the UI and payment elements.

Clone and Install:

git clone [FRONTEND_REPO_URL] crave-frontend
cd crave-frontend
npm install


Create .env File: (Only one variable is strictly required for the client).

VITE_STRIPE_PUBLIC_KEY=pk_test_...


Run the Client:

npm run dev


The application will be accessible at http://localhost:5173.

🔒 Role-Based Access Credentials

Use these accounts to test the different functionalities:

Role

Email

Password

Access

SuperAdmin

admin@crave.com

admin123

Analytics, Menu Management, Full Queue Control

Kitchen Manager

chef@crave.com

password123

KDS (Queue management up to 'Ready' status)

Customer

(Register a new account)



Ordering, My Orders, Loyalty Wallet

🌐 Deployment Pipeline

The project is designed for production deployment using continuous integration/continuous deployment (CI/CD) services:

Service

Purpose

Build Command

Start Command

Render (Backend)

Host API & WebSockets

npm install

node src/server.js

Vercel (Frontend)

Host Static React App

npm run build

(Serves static files from dist folder)

Developed by Ayush Thakare as a demonstration of high-performance full-stack architecture.
