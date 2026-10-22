----------------------------------------
# Multi-Vendor eCommerce Web Application
----------------------------------------

A secure, production-ready multi-vendor eCommerce platform built with Django and backed by a MariaDB database. This application is designed to support multiple user roles, robust inventory management, dynamic carts, automated invoice generation, token-based security, and a dual verified/unverified review system.

-------------------------------------------------
# Key Features & Requirements Fulfilled
-------------------------------------------------
 
1. Custom Role-Based Authentication:
   - Distinct user roles for Buyers and Vendors upon registration.
   - Role-specific permissions restrict product creation and store management strictly to vendors, while allowing buyers to browse, cart, checkout, and review.
 
2. Session-Based Shopping Cart:
   - Fully persistent, lightweight shopping cart stored within Django sessions (request.session['cart']), allowing users to manage items seamlessly without database clutter prior to checkout.
 
3. Automated Checkout & Email Invoicing:
   - Secure checkout processing that atomically creates orders, clears the session cart, itemizes purchased products, and dispatches a comprehensive invoice directly to the buyer's email address.
 
4. Verified & Unverified Product Reviews:
   - Universal review submission allowing any registered user to leave feedback.
   - Automated backend validation queries past order history to dynamically flag reviews as Verified Purchase or Unverified Review.
 
5. Secure Password Recovery & Expiring Tokens:
   - Built-in Django cryptographic token generation (`PasswordResetView`) that dispatches secure recovery links with strict expiration timeouts (defaulting to a secure 3-day window) to prevent token replay attacks.
 
6. MariaDB Backend & Migrations:
   - Configured with `django.db.backends.mysql` utilizing 64-bit integer fields (`BigAutoField`) to ensure full structural integrity and prevent MariaDB foreign key (`Errno 150`) constraints during migration.

---------------
# Tech Stack
---------------
- Backend: Python, Django
- Database: MariaDB / MySQL
- Frontend: Bootstrap 5, HTML5, CSS3, Django Template Engine
- Authentication: Django Auth Framework & Cryptographic Tokens

---------------
# Prerequisites
---------------
Make sure you have the following installed on your system:
- Python (version 3.14.4)
- MariaDB / MySQL server

----------------------------------
# Installation & Local Setup Guide
----------------------------------

Follow these steps to set up and run the project locally on your machine:

1. Clone or Extract the Project
    - Clone the project from your GitHub profile and enter the project folder
    ```bash
    
    git clone [https://github.com/mcusick001/Django-eCommerce-Application-Part-1]
    
    cd NEW-Django-eCommerce-Part1
    ```

2. Set Up a Virtual Environment & Install Dependencies
    ```bash
    
    python -m venv venv

    venv\Scripts\Activate.ps1

    pip install -r requirements.txt
    ```

3. Configure the Environmental Variables
    - Windows (Command Prompt):
    ```cmd

    copy .env.example .env
    ```
    - Open the newly created .env file in your code editor and update
      the database username, password, and secret key to match your
      local environment.
      
4. Log into your MariaDB shell and create the database:
    ```bash

    mysql -u root -p
    ```
    - Once logged in, run the following SQL commands to create the
      database and user:
    ```sql

    CREATE DATABASE ecommerce_db;
    CREATE USER 'shop_user'@'localhost' IDENTIFIED BY 'password123';
    GRANT ALL PRIVILEGES ON ecommerce_db.* TO 'shop_user'@'localhost';
    FLUSH PRIVILEGES;
    EXIT;
    ``` 

5. Run Database Migrations
    - Apply the Django schema to your MariaDB instance:
    ```bash:

    python manage.py makemigrations
    python manage.py migrate
    ```

6. Create an Administrator (Superuser) Account
    ```bash:

    python manage.py createsuperuser
    ```
    - Follow the prompts to enter username, email, and password.

7. Run the deployment server
    ```bash:

    python manage.py runserver
    ```
    - Open your brower and navigate to [http://127.0.0.1:8000/]
    to use the application!
