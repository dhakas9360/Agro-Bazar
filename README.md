
# 🌾 Agro-Bazar (E-Mandi) - Agricultural Marketplace Platform

**Agro-Bazar** is a comprehensive digital agricultural marketplace platform that connects farmers, wholesellers, and retailers in one unified ecosystem. Built as an online e-Mandi system, it enables transparent and efficient trading of agricultural products while eliminating traditional intermediaries.

## 📖 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Installation & Setup](#installation--setup)
- [Database Schema](#database-schema)
- [User Roles & Functionality](#user-roles--functionality)
- [API Endpoints](#api-endpoints)
- [File Structure](#file-structure)
- [Screenshots](#screenshots)
- [Contributing](#contributing)
- [License](#license)

## 🌟 Overview

Agro-Bazar (E-Mandi) is an online platform that revolutionizes traditional agricultural trading. Inspired by India's National Agriculture Market (e-NAM) initiative, this platform provides:

- **Direct connection** between farmers and buyers
- **Transparent pricing** through online auctions
- **Reduced intermediary costs** for better farmer profits
- **Digital marketplace** accessible from anywhere
- **Multi-role support** for farmers, wholesellers, and retailers

The platform addresses the challenges of traditional mandi systems where farmers often receive lower prices due to multiple intermediaries and handling costs.

## ✨ Features

### 🎯 Core Features
- **User Authentication & Authorization** - Secure login/registration with role-based access
- **Multi-role Support** - Farmer, Wholeseller, Retailer, and Admin roles
- **Product Listing Management** - Add, update, delete agricultural products
- **Shopping Cart System** - Add products to cart and manage quantities
- **Real-time Inventory Management** - Track stock levels and availability
- **State-wise User Management** - Location-based user categorization
- **Admin Dashboard** - Comprehensive admin panel for platform management

### 🛒 E-commerce Features
- Product catalog with images and descriptions
- Price comparison across different sellers
- Inventory tracking and stock management
- Shopping cart and checkout system
- User profile management

### 👥 User Management
- Role-based access control (Farmer/Wholeseller/Retailer/Admin)
- User registration with state information
- Profile management and listing history
- Secure password encryption using bcrypt

## 🔧 Technology Stack

### Backend
- **Node.js** - Server-side JavaScript runtime
- **Express.js** - Web application framework
- **MySQL** - Relational database management
- **Passport.js** - Authentication middleware
- **bcrypt** - Password hashing and security

### Frontend
- **EJS** - Embedded JavaScript templating
- **Bootstrap** - Responsive CSS framework
- **jQuery** - JavaScript library for DOM manipulation
- **AOS** - Animate On Scroll library
- **Owl Carousel** - Touch enabled jQuery plugin

### Database
- **MySQL2** - MySQL client for Node.js
- **Connection pooling** for optimized database performance

## 🏗️ System Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│     Frontend    │    │     Backend     │    │    Database     │
│                 │    │                 │    │                 │
│   EJS Templates │◄──►│   Express.js    │◄──►│     MySQL       │
│   Bootstrap UI  │    │   Passport Auth │    │   Users Table   │
│   jQuery/JS     │    │   Route Handlers│    │   Products      │
│                 │    │   File Upload   │    │   Cart System   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 🚀 Installation & Setup

### Prerequisites
- **Node.js** (v12 or higher)
- **MySQL** (v5.7 or higher)
- **npm** (comes with Node.js)

### Step-by-Step Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/dhakas9360/Agro-Bazar.git
   cd Agro-Bazar
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure Database**
   
   Edit the database configuration in `config/database.js`:
   ```javascript
   module.exports = {
       'connection': {
           'host': 'localhost',
           'user': 'your_mysql_username',
           'password': 'your_mysql_password'
       },
       'database': 'my_schema',
       'users_table': 'users'
   };
   ```

4. **Create Database Schema**
   ```bash
   node scripts/create_database.js
   ```

5. **Launch the Application**
   ```bash
   node server.js
   ```
   or
   ```bash
   npm start
   ```

6. **Access the Application**
   
   Open your browser and visit: `http://localhost:8080`

## 🗄️ Database Schema

### Users Table
```sql
CREATE TABLE users (
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    username VARCHAR(20) NOT NULL UNIQUE,
    password CHAR(60) NOT NULL,
    role CHAR(60) NOT NULL,
    state CHAR(60) NOT NULL,
    PRIMARY KEY (id)
);
```

### Farmer/Wholeseller/Retailer Tables
```sql
CREATE TABLE Farmer (
    id INT UNSIGNED NOT NULL,
    title VARCHAR(255) NOT NULL,
    image VARCHAR(250),
    price INT,
    stock INT,
    FOREIGN KEY (id) REFERENCES users(id)
);
```

### Cart Table
```sql
CREATE TABLE Cart (
    id INT UNSIGNED NOT NULL,
    title VARCHAR(255) NOT NULL,
    image VARCHAR(250),
    price INT NOT NULL,
    quantity INT NOT NULL,
    sellerID INT UNSIGNED NOT NULL,
    FOREIGN KEY (id) REFERENCES users(id),
    FOREIGN KEY (sellerID) REFERENCES users(id)
);
```

## 👤 User Roles & Functionality

### 🌾 Farmer
- Register as a farmer with state information
- List agricultural products with images, prices, and stock
- Update product listings and inventory
- View and manage their product portfolio
- Track sales and buyer interactions

### 🏪 Wholeseller
- Register as a wholeseller
- List bulk agricultural products
- Manage large-scale inventory
- Set competitive pricing for bulk purchases
- Handle B2B transactions

### 🛍️ Retailer
- Register as a retailer
- Browse and purchase from farmers and wholesellers
- Manage shopping cart and orders
- Track purchase history
- Access retail-specific product listings

### 👨‍💼 Administrator
- Monitor all platform activities
- Manage user accounts across all roles
- View comprehensive reports
- Moderate product listings
- Handle platform maintenance

## 🛣️ API Endpoints

### Authentication Routes
- `GET /` - Home page with product listings
- `GET /login` - Login page
- `POST /login` - Process login
- `GET /signup` - Registration page
- `POST /signup` - Process registration
- `GET /logout` - User logout

### Product Management
- `GET /addListing` - Add new product listing
- `POST /addListing` - Process new listing
- `GET /updateListing/:title/:price/:stock` - Update product form
- `POST /updateListing` - Process product update
- `GET /deleteListing/:title/:price/:stock` - Delete product

### Cart Management
- `POST /addToCart` - Add item to cart
- `GET /cart` - View shopping cart
- `GET /deleteItemCart/:id/:sellerID/:title/:quantity/:price/:image` - Remove cart item

### User Profile
- `GET /profile` - User profile page
- `GET /admin` - Admin dashboard

## 📁 File Structure

```
Agro-Bazar/
├── 📁 app/
│   └── routes.js              # Application routes and logic
├── 📁 config/
│   ├── database.js            # Database configuration
│   └── passport.js            # Authentication configuration
├── 📁 scripts/
│   ├── create_database.js     # Database initialization
│   └── filling.js             # Data seeding script
├── 📁 views/                  # EJS templates
│   ├── index.ejs              # Homepage
│   ├── login.ejs              # Login page
│   ├── signup.ejs             # Registration page
│   ├── profile.ejs            # User profile
│   ├── cart.ejs               # Shopping cart
│   ├── admin.ejs              # Admin dashboard
│   ├── addListing.ejs         # Add product form
│   ├── updateListing.ejs      # Update product form
│   ├── shop.ejs               # Product catalog
│   ├── about.ejs              # About page
│   ├── contact.ejs            # Contact page
│   └── 📁 css/               # Stylesheets
│   └── 📁 js/                # Client-side JavaScript
│   └── 📁 images/            # Static images
├── 📁 modist/                 # Additional frontend assets
├── server.js                  # Main application server
├── package.json               # Project dependencies
├── database.sql               # Database schema
└── README.md                  # Project documentation
```

## 🖼️ Screenshots

The platform includes several key pages:

- **Homepage** - Product showcase with featured listings
- **Login/Registration** - Secure user authentication
- **User Dashboard** - Role-specific user interface
- **Product Management** - Add/edit/delete listings
- **Shopping Cart** - E-commerce functionality
- **Admin Panel** - Platform administration tools

## 🤝 Contributing

We welcome contributions to improve Agro-Bazar! Here's how you can help:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/AmazingFeature`)
3. **Commit your changes** (`git commit -m 'Add some AmazingFeature'`)
4. **Push to the branch** (`git push origin feature/AmazingFeature`)
5. **Open a Pull Request**

### Development Guidelines
- Follow existing code style and conventions
- Add comments for complex logic
- Test your changes thoroughly
- Update documentation as needed

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 🆘 Support & Contact

For support, feature requests, or bug reports:

- **Repository**: [GitHub - Agro-Bazar](https://github.com/dhakas9360/Agro-Bazar)
- **Issues**: [GitHub Issues](https://github.com/dhakas9360/Agro-Bazar/issues)

## 🙏 Acknowledgments

- Inspired by India's National Agriculture Market (e-NAM) initiative
- Built to support farmers and improve agricultural trade efficiency
- Thanks to all contributors and the open-source community

---

**Made with ❤️ for farmers and agricultural communities**

