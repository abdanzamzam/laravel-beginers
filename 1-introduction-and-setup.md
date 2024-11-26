
# Laravel Tutorial for Beginners: #1 - Introduction & Setup

## **What is Laravel?**
Laravel is a free, open-source PHP web framework designed to make web development simpler and more efficient. It follows the **Model-View-Controller (MVC)** architectural pattern and provides tools and features for tasks such as routing, authentication, sessions, and caching.

Laravel is known for:
- **Elegance**: Simplified syntax for writing cleaner and more maintainable code.
- **Powerful tools**: Built-in features like Eloquent ORM, Blade templating, and migrations.
- **Community support**: Extensive documentation and an active community.

---

## **Why Use Laravel?**
1. **Modern and Secure**: Laravel includes tools for password hashing, encryption, and user authentication.
2. **Efficient Development**: With built-in tools for routing, database management, and templates, it reduces repetitive coding.
3. **Rich Ecosystem**: Laravel has various packages like Laravel Sanctum for API tokens, Laravel Breeze for starter kits, and Laravel Horizon for managing queues.

---

## **Setup Laravel on Your System**

### **1. System Requirements**
Before installing Laravel, ensure your system meets the following requirements:
- **PHP version**: 8.1 or higher
- **Composer**: A dependency manager for PHP
- **Web server**: Apache or Nginx
- **Database**: MySQL, PostgreSQL, SQLite, or SQL Server

You can verify your PHP version by running:
```bash
php -v
```

### **2. Install Composer**
Composer is required to install Laravel and manage its dependencies.

- **On Windows**:
  Download the Composer installer from [getcomposer.org](https://getcomposer.org/).

- **On macOS/Linux**:
  Run this command in your terminal:
  ```bash
  curl -sS https://getcomposer.org/installer | php
  sudo mv composer.phar /usr/local/bin/composer
  ```

Verify the installation:
```bash
composer -v
```

### **3. Install Laravel**
Once Composer is installed, you can create a new Laravel project in two ways:

- **Using Laravel Installer**:
  1. Install the Laravel installer globally:
     ```bash
     composer global require laravel/installer
     ```
  2. Create a new project:
     ```bash
     laravel new project_name
     ```

- **Using Composer Create-Project**:
  1. Run:
     ```bash
     composer create-project --prefer-dist laravel/laravel project_name
     ```

Move into the project directory:
```bash
cd project_name
```

### **4. Run the Laravel Development Server**
Start the built-in development server by running:
```bash
php artisan serve
```

Visit `http://127.0.0.1:8000` in your web browser to see the default Laravel welcome page.

---

## **Laravel Folder Structure Overview**
Once you create a Laravel project, you’ll notice a structured set of directories. Here’s a brief explanation:

- **app/**: Contains the core application logic (controllers, models, middleware, etc.).
- **bootstrap/**: Initializes the framework.
- **config/**: Configuration files for your application (e.g., database, mail, etc.).
- **database/**: Migrations, seeders, and database factories.
- **resources/**: Views, Blade templates, and assets like CSS/JS.
- **routes/**: Defines web, API, console, and channel routes.
- **storage/**: Stores logs, compiled Blade views, and file uploads.
- **vendor/**: Contains all Composer dependencies.

---

## **Key Laravel Concepts**

### **1. Artisan CLI**
Laravel includes a command-line tool called Artisan, which simplifies tasks like generating code and managing databases.

Some useful Artisan commands:
- Run the development server:
  ```bash
  php artisan serve
  ```
- Create a new controller:
  ```bash
  php artisan make:controller ControllerName
  ```
- Run database migrations:
  ```bash
  php artisan migrate
  ```

### **2. Configuration**
Laravel uses environment files (`.env`) to manage application settings like database credentials, mail configurations, and more. Example of a `.env` file:
```env
APP_NAME=LaravelApp
APP_ENV=local
APP_KEY=base64:keyhere
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
```

### **3. Routing**
Laravel’s routing system allows you to define application URLs. You’ll work with the `routes/web.php` file for web routes.

Example route:
```php
Route::get('/', function () {
    return view('welcome');
});
```

---

## **Next Steps**
Now that Laravel is installed and running, the next step is to learn about **routes** and **views**, which are essential to building a functional web application.

Stay tuned for the next topic: **Routes & Views**!
