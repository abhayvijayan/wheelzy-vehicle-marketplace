# 🚗 Wheelzy – Vehicle Marketplace

**Wheelzy** is a full-stack vehicle marketplace web application designed to connect vehicle buyers and sellers through a centralized digital platform. Users can browse available vehicles, publish their own listings, save favorites, and submit purchase requests. A dedicated administration panel provides tools for managing users, vehicle listings, and purchase requests.

## 📌 Overview

Buying and selling vehicles can involve searching across multiple platforms, communicating with sellers, and managing inquiries manually. Wheelzy aims to simplify this process by bringing vehicle listings and buyer–seller interactions together in one application.

The project combines a web-based client, a backend REST API, a MySQL database, and a separate administration interface.

## ✨ Features

### 👤 User Management

- User registration and login.
- JWT-based authentication.
- Profile viewing and editing.
- Password hashing during user registration.
- Personal vehicle listing management.

### 🚘 Vehicle Marketplace

- Browse available and approved vehicle listings.
- View vehicle details, images, descriptions, and prices.
- Search vehicles by title, year, location, and description.
- Publish new vehicle listings.
- Edit or delete your own listings.
- Update vehicle availability status.

### ❤️ Favorites

- Add vehicles to a favorites list.
- View saved vehicles.
- Remove vehicles from favorites.

### 📩 Purchase Requests

- Submit purchase requests with a message and contact information.
- View requests submitted by the current user.
- View inquiries received for your own vehicle listings.
- Manage and delete purchase requests.

### 🛠️ Administration Panel

- Dedicated administrator interface.
- Administrator login.
- View and manage vehicle listings.
- Approve or decline vehicle listings.
- View, update, and delete user records.
- Review purchase requests and related buyer, seller, and vehicle information.

## 🛠️ Technology Stack

| Component | Technologies |
|---|---|
| Client | HTML, JavaScript, Tailwind CSS |
| Admin panel | React, Vite, React Router |
| Backend | Node.js, Express.js |
| Database | MySQL |
| Database query builder | Knex.js |
| Authentication | JSON Web Tokens (JWT) |
| Password hashing | bcrypt |
| HTTP requests | Axios |
| Development tools | npm, Nodemon, Git, GitHub |

## 🏗️ Project Architecture

The application is organized into three main components:

```text
vehicle-marketplace/
│
├── client/                 # User-facing web application
│   ├── index.html
│   ├── login.html
│   ├── signup.html
│   ├── vehicle-details.html
│   ├── add-vehicle.html
│   ├── my-listings.html
│   ├── profile.html
│   └── requests.html
│
├── admin/                  # Administration interface
│   ├── src/
│   ├── package.json
│   └── vite.config.js
│
├── server/                 # Backend REST API
│   ├── configs/
│   │   └── database.js
│   ├── middlewares/
│   ├── routes/
│   │   ├── auth.routes.js
│   │   ├── vehicle.routes.js
│   │   ├── user.routes.js
│   │   ├── favorite.routes.js
│   │   ├── request.routes.js
│   │   └── admin.routes.js
│   ├── server.js
│   └── package.json
│
├── admin.bat
├── server.bat
└── open_in_vs.bat
```

*This tree highlights the main application components; consult the repository for the complete and current file structure.*

## 🔄 Application Workflow

1. A user registers or logs in to the platform.
2. The user browses available vehicle listings.
3. A seller adds a vehicle with its details, price, location, and image.
4. The administrator reviews the listing and approves or declines it.
5. Approved vehicles appear in the public marketplace.
6. Interested buyers can save vehicles to favorites or submit purchase requests.
7. Sellers can view inquiries related to their listings.
8. Administrators can manage users, listings, and requests.

## 🚀 Getting Started

### Prerequisites

Install the following software before running the application:

- [Node.js](https://nodejs.org/) and npm
- [MySQL Community Server](https://dev.mysql.com/downloads/mysql/)
- A code editor such as [Visual Studio Code](https://code.visualstudio.com/)
- A browser such as Chrome or Firefox

### 1. Clone the repository

```bash
git clone https://github.com/abhayvijayan/whelzy-vehicle-marketplace.git
cd wheelzy-vehicle-marketplace
```

### 2. Configure the database

Create a MySQL database named `vehicle_sell`.

```sql
CREATE DATABASE vehicle_sell;
```

The backend database configuration is located at:

```text
server/configs/database.js
```

Configure the MySQL host, port, username, password, and database name to match your local environment.

**Note:** The current database configuration uses local MySQL credentials directly in the source code. Update these settings for your environment and avoid committing real credentials.

Create or import the required database tables before starting the backend. The application expects tables for user credentials, vehicles, favorites, purchase requests, and administrators.

### 3. Configure environment variables

Create a `.env` file inside the `server` directory:

```env
PORT=5000
JWT_SECRET=replace_with_a_long_random_secret
```

The server uses `PORT` with a fallback of `5000` and `JWT_SECRET` for token signing. Keep secrets private and use a strong, randomly generated JWT secret.

### 4. Install and run the backend

Open a terminal:

```bash
cd server
npm install
npm run dev
```

The backend should start on:

```text
http://localhost:5000
```

The development script uses Nodemon to restart the server when files change.

### 5. Run the client

The client is a collection of HTML and JavaScript files rather than a separate npm application.

Open the `client` directory in Visual Studio Code and launch `index.html` using the Live Server extension, or serve the directory using another local static HTTP server.

For compatibility with the current backend CORS configuration, use:

```text
http://127.0.0.1:5500
```

The client currently sends API requests to `http://localhost:5000`.

### 6. Run the administration panel

Open another terminal:

```bash
cd admin
npm install
npm run dev
```

Vite will display the local URL for the administration interface in the terminal.

## 🔌 Backend API Overview

The backend exposes REST API routes under the following prefixes:

| Prefix | Purpose |
|---|---|
| `/api/auth` | User registration, login, and token verification |
| `/api/vehicles` | Vehicle listing, retrieval, editing, deletion, and availability |
| `/api/users` | User profile and favorite-related operations |
| `/api/favorites` | Add, view, and remove favorites |
| `/api/requests` | Submit and retrieve purchase requests |
| `/api/admin` | Administrative authentication and management operations |

### Selected endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/auth/register` | Register a user |
| `POST` | `/api/auth/login` | Authenticate a user |
| `GET` | `/api/auth/verifytoken` | Verify a JWT |
| `GET` | `/api/vehicles` | Retrieve approved vehicles |
| `POST` | `/api/vehicles/add` | Create a vehicle listing |
| `GET` | `/api/vehicles/my` | Retrieve the current user's listings |
| `PUT` | `/api/vehicles/edit/:id` | Update an owned listing |
| `DELETE` | `/api/vehicles/delete/:id` | Delete an owned listing |
| `POST` | `/api/favorites/add` | Add a vehicle to favorites |
| `POST` | `/api/requests/send` | Submit a purchase request |
| `GET` | `/api/requests/my-requests` | Retrieve submitted requests |
| `POST` | `/api/admin/login` | Administrator login |
| `PUT` | `/api/admin/vehicles/:id/approve` | Approve or decline a listing |

Protected user endpoints require a bearer token in the `Authorization` header:

```http
Authorization: Bearer YOUR_JWT_TOKEN
```

These endpoints are based on the backend route definitions. Request bodies, permissions, and response formats should be checked in the corresponding route files.

## 🔐 Security Considerations

Before using the application in a production environment, review the following:

- Move database credentials into environment variables.
- Hash administrator passwords and verify them using a secure password-hashing method.
- Protect administrative endpoints with authentication and authorization middleware.
- Validate and sanitize incoming request data.
- Restrict access to user records and purchase requests according to user roles.
- Configure CORS for the intended deployment domains.
- Avoid returning internal exception details to clients.

## 🔮 Future Enhancements

Potential improvements include:

- Advanced filtering by make, model, price, year, and location.
- Vehicle comparison functionality.
- Image upload and validation.
- Notifications for new purchase requests and listing approvals.
- Improved administrative analytics.
- Pagination for large numbers of listings.
- Automated backend testing and API documentation.
- Enhanced role-based access control.

## 🎓 Project Purpose

Wheelzy is a software development project that demonstrates the practical application of frontend development, REST API design, database integration, authentication, and administrative workflows in an online marketplace.

It provides a foundation for exploring full-stack web development and designing systems that facilitate interactions between buyers and sellers.

## 👨‍💻 Author

**Abhay Vijayan**

GitHub: [@abhayvijayan](https://github.com/abhayvijayan)

## 📄 License

No license has been specified in this README. Refer to the repository's `LICENSE` file for applicable usage and distribution terms.

---

*Wheelzy — Bringing vehicle buyers and sellers together.*
