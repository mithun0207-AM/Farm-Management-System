# 🌾 Farm Management System

> A full-stack web application for managing farmer registrations, agro-products, and agricultural operations — built with **Python Flask** and **MySQL**.

---

## 📌 Table of Contents

- [About the Project](#-about-the-project)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Database Schema](#-database-schema)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Database Setup](#database-setup)
  - [Run the Application](#run-the-application)
- [Usage](#-usage)
- [Screenshots](#-screenshots)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🌿 About the Project

The **Farm Management System** is a DBMS mini-project designed to digitize and streamline farm operations. It provides a centralized platform where authenticated users can register farmers, manage agro-products, and automatically log all database activities using **MySQL Triggers**.

This project was developed as part of a **Database Management Systems (DBMS)** course mini-project.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔐 **User Authentication** | Secure signup and login with session management via Flask-Login |
| 👨‍🌾 **Farmer Registration** | Add, view, edit, and delete farmer records with full CRUD support |
| 🌱 **Agro Products** | List and add agricultural products with descriptions and pricing |
| 📋 **Audit Triggers** | MySQL triggers automatically log all INSERT, UPDATE, and DELETE operations |
| 📊 **Reports** | Pre-generated farm reports available in PDF format |
| 🔗 **Database Test Route** | Built-in `/test` endpoint to verify database connectivity |
| 📬 **Contact Form** | User-facing contact page with flash message feedback |

---

## 🛠 Tech Stack

**Backend**
- Python 3.x
- Flask
- Flask-SQLAlchemy
- Flask-Login
- Werkzeug

**Frontend**
- HTML5 / CSS3
- Bootstrap 5
- jQuery
- Font Awesome
- AOS (Animate on Scroll)
- Owl Carousel

**Database**
- MySQL / MariaDB
- phpMyAdmin (recommended for setup)

---

## 🗄 Database Schema

The `farmers` database contains the following tables:

```
farmers/
├── user              → Stores registered application users
├── register          → Stores farmer details (name, age, gender, phone, address, farming type)
├── addagroproducts   → Stores agro-product listings
├── farming           → Lookup table for farming types
├── trig              → Audit log table populated by MySQL triggers
└── test              → Simple connectivity test table
```

### 🔁 MySQL Triggers

Three triggers are defined on the `register` table to automatically log all farmer record changes into the `trig` table:

| Trigger Name | Event | Timing | Action |
|---|---|---|---|
| `insertion` | INSERT | AFTER | Logs new farmer record |
| `updation` | UPDATE | AFTER | Logs farmer record update |
| `deletion` | DELETE | BEFORE | Logs farmer record deletion |

---

## 📁 Project Structure

```
Farm-management-system/
├── farmer system/
│   ├── main.py                  # Main Flask application & all routes
│   ├── farmers.sql              # Full MySQL database dump (schema + data)
│   ├── backups/
│   │   ├── farmers.sql.bak      # Database backup
│   │   └── farming.html.bak     # HTML backup
│   ├── static/
│   │   ├── assets/
│   │   │   ├── css/             # Custom stylesheets
│   │   │   ├── js/              # Custom JavaScript
│   │   │   └── vendor/          # Third-party libraries (Bootstrap, jQuery, etc.)
│   │   ├── css/                 # Additional page-specific styles
│   │   └── images/              # Static images (background, etc.)
│   └── templates/               # Jinja2 HTML templates
│       ├── base.html            # Base layout template
│       ├── index.html           # Home page
│       ├── login.html           # Login page
│       ├── signup.html          # Sign up page
│       ├── farmer.html          # Register a farmer
│       ├── farmerdetails.html   # View all farmer records
│       ├── edit.html            # Edit farmer record
│       ├── agroproducts.html    # View agro products
│       ├── addagroproducts.html # Add agro product
│       ├── contact.html         # Contact page
│       └── about.html           # About page
└── farm reports/
    ├── report-1.pdf             # Farm report 1
    └── report2.pdf              # Farm report 2
```

---

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed:

- [Python 3.8+](https://www.python.org/downloads/)
- [MySQL](https://dev.mysql.com/downloads/) or [XAMPP](https://www.apachefriends.org/) (includes MySQL + phpMyAdmin)
- [pip](https://pip.pypa.io/en/stable/)
- Git

---

### Installation

**1. Clone the repository**

```bash
git clone https://github.com/mithun0207-AM/Farm-Management-System.git
cd Farm-management-system/farmer\ system
```

**2. Create and activate a virtual environment** *(recommended)*

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS / Linux
python3 -m venv venv
source venv/bin/activate
```

**3. Install required Python packages**

```bash
pip install flask flask-sqlalchemy flask-login werkzeug
```

---

### Database Setup

**1. Start your MySQL server**

If using XAMPP, open the XAMPP Control Panel and start the **Apache** and **MySQL** modules.

**2. Create the database**

Open [phpMyAdmin](http://localhost/phpmyadmin) in your browser and:
1. Click **New** in the left panel
2. Name the database `farmers`
3. Click **Create**

**3. Import the SQL dump**

1. Select the `farmers` database in phpMyAdmin
2. Click the **Import** tab
3. Choose the file: `farmer system/farmers.sql`
4. Click **Go**

Alternatively, via the MySQL command line:
```bash
mysql -u root -p farmers < "farmer system/farmers.sql"
```

**4. Configure the database URI in `main.py`**

Open `main.py` and update the connection string if needed:

```python
# Default configuration (no password for root)
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://root:@localhost/farmers'

# If your root user has a password:
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://root:YOUR_PASSWORD@localhost/farmers'
```

---

### Run the Application

```bash
python main.py
```

The app will start in **debug mode** and be accessible at:

```
http://127.0.0.1:5000
```

To verify database connectivity, visit:

```
http://127.0.0.1:5000/test
```

You should see: `My database is Connected`

---

## 📖 Usage

| Route | Access | Description |
|---|---|---|
| `/` | Public | Home / landing page |
| `/signup` | Public | Create a new account |
| `/login` | Public | Log into your account |
| `/logout` | Logged in | Log out of your session |
| `/register` | Logged in | Register a new farmer |
| `/farmerdetails` | Logged in | View all registered farmers |
| `/edit/<id>` | Logged in | Edit a farmer's details |
| `/delete/<id>` | Logged in | Delete a farmer record |
| `/agroproducts` | Public | Browse agro products |
| `/addagroproduct` | Logged in | Add a new agro product |
| `/contact` | Public | Contact form |
| `/test` | Public | Check database connection |

---

## 🤝 Contributing

Contributions are welcome! To get started:

1. Fork this repository
2. Create a new branch: `git checkout -b feature/your-feature-name`
3. Make your changes and commit: `git commit -m "Add your feature"`
4. Push to the branch: `git push origin feature/your-feature-name`
5. Open a Pull Request

---

## ⚠️ Known Issues & Future Improvements

- [ ] Passwords are currently stored as plain text — replace with hashed passwords using `werkzeug.security`
- [ ] Add server-side form validation
- [ ] Implement role-based access control (admin vs. farmer)
- [ ] Add search and filter functionality to farmer details page
- [ ] Deploy to a production server (e.g., Heroku, Render, or AWS)

---

## 📄 License

This project is created for **educational purposes** as a DBMS mini-project. Feel free to use, modify, and distribute with attribution.

---

<div align="center">
  Made with ❤️ using Flask & MySQL
</div>
