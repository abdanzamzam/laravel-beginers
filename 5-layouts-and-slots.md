
# Laravel Tutorial for Beginners: #5 - Layouts & Slots

---

## **What are Layouts in Laravel?**
Layouts in Laravel help you define a consistent structure or template for your views. They allow you to reuse common HTML elements (like headers, footers, and navigation bars) across multiple pages, keeping your code DRY (Don't Repeat Yourself).

## **What are Slots?**
Slots in Blade are placeholders in layouts where dynamic content can be injected. They provide a way to customize specific sections of a layout for different views.

---

## **Creating a Layout**
Layouts in Laravel are typically stored in the `resources/views/layouts` directory.

### **Example: Creating a Layout**
1. Create a file named `app.blade.php` in the `resources/views/layouts` directory.
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>@yield('title')</title>
       <link rel="stylesheet" href="/css/app.css">
   </head>
   <body>
       <header>
           <h1>My Laravel App</h1>
       </header>

       <main>
           @yield('content')
       </main>

       <footer>
           <p>&copy; 2024 My Laravel App</p>
       </footer>
   </body>
   </html>
   ```

- **`@yield('title')`**: Placeholder for the page title.
- **`@yield('content')`**: Placeholder for the main content.

---

## **Extending a Layout**
To use the layout, you extend it in your views using the `@extends` directive.

### **Example: Using a Layout**
1. Create a view file named `home.blade.php` in the `resources/views` directory:
   ```php
   @extends('layouts.app')

   @section('title', 'Home Page')

   @section('content')
       <h2>Welcome to My Laravel App!</h2>
       <p>This is the home page.</p>
   @endsection
   ```

- **`@extends`**: Specifies the layout to extend.
- **`@section`**: Defines content for specific placeholders in the layout.

---

## **Using Slots for Components**
Blade components allow you to define reusable elements with slots for dynamic content.

### **Example: Creating a Component with Slots**
1. Create a component file in `resources/views/components` named `alert.blade.php`:
   ```html
   <div class="alert alert-{{ $type }}">
       {{ $slot }}
   </div>
   ```

2. Use the component in a view:
   ```php
   <x-alert type="success">
       Operation completed successfully!
   </x-alert>

   <x-alert type="danger">
       An error occurred!
   </x-alert>
   ```

- **`$type`**: Dynamic variable passed to the component.
- **`{{ $slot }}`**: Placeholder for the content inside the component.

---

## **Master Layout Example**
### **Master Layout: `layouts/master.blade.php`**
```html
<!DOCTYPE html>
<html>
<head>
    <title>@yield('title')</title>
    <link rel="stylesheet" href="/css/app.css">
</head>
<body>
    <header>
        <h1>Website Header</h1>
        <nav>
            <ul>
                <li><a href="/">Home</a></li>
                <li><a href="/about">About</a></li>
                <li><a href="/contact">Contact</a></li>
            </ul>
        </nav>
    </header>

    <div class="container">
        @yield('content')
    </div>

    <footer>
        <p>&copy; 2024 My Laravel App</p>
    </footer>
</body>
</html>
```

### **Child View: `home.blade.php`**
```php
@extends('layouts.master')

@section('title', 'Home Page')

@section('content')
    <h2>Welcome Home</h2>
    <p>This is the content of the home page.</p>
@endsection
```

---

## **Nested Sections**
You can nest sections to provide more granularity.

### **Example: Nested Sections**
1. Add nested placeholders in the layout:
   ```html
   <main>
       <h1>@yield('header')</h1>
       @yield('content')
   </main>
   ```

2. Define nested sections in a view:
   ```php
   @section('header', 'Welcome Home')

   @section('content')
       <p>This is the content of the home page.</p>
   @endsection
   ```

---

## **Key Points**
1. Layouts define reusable templates for your views, reducing repetitive code.
2. Use `@yield` to define placeholders in layouts and `@section` to provide content in views.
3. Components with slots enable dynamic content in reusable UI elements.
4. Use `@extends` to inherit layouts and `@slot` for passing content to components.

---

This tutorial provides a complete guide to using layouts and slots in Laravel.
