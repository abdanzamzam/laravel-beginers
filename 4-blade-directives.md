
# Laravel Tutorial for Beginners: #4 - Blade Directives

---

## **What are Blade Directives?**
Blade is Laravel's powerful templating engine that simplifies creating dynamic views. Blade directives are special functions or keywords that enable you to perform tasks like conditionals, loops, and more within your views. They make your templates cleaner and more readable.

---

## **Common Blade Directives**

### **1. Echoing Variables**
Blade allows you to display data using the `{{ }}` syntax.

#### **Example: Echoing a Variable**
```php
<h1>Welcome, {{ $name }}</h1>
```
- Automatically escapes HTML to prevent XSS attacks.

For raw output (no escaping), use:
```php
<h1>{!! $rawHtml !!}</h1>
```

---

### **2. Conditionals**

#### **`@if` Directive**
Used for conditionally displaying content.
```php
@if ($age >= 18)
    <p>You are an adult.</p>
@else
    <p>You are a minor.</p>
@endif
```

#### **`@isset` Directive**
Checks if a variable is set and not `null`.
```php
@isset($user)
    <p>User is logged in: {{ $user->name }}</p>
@endisset
```

#### **`@empty` Directive**
Checks if a variable is empty.
```php
@empty($posts)
    <p>No posts available.</p>
@endempty
```

#### **`@unless` Directive**
Runs the block unless the condition is true.
```php
@unless($isAdmin)
    <p>You do not have admin privileges.</p>
@endunless
```

---

### **3. Loops**

#### **`@foreach` Directive**
Iterates through an array or collection.
```php
@foreach ($posts as $post)
    <h2>{{ $post->title }}</h2>
    <p>{{ $post->content }}</p>
@endforeach
```

#### **`@for` Directive**
Standard `for` loop.
```php
@for ($i = 0; $i < 5; $i++)
    <p>Index: {{ $i }}</p>
@endfor
```

#### **`@while` Directive**
Runs as long as the condition is true.
```php
@while ($count < 3)
    <p>Count: {{ $count }}</p>
    @php $count++; @endphp
@endwhile
```

#### **`@forelse` Directive**
Iterates through a collection, but provides a fallback if it's empty.
```php
@forelse ($comments as $comment)
    <p>{{ $comment->text }}</p>
@empty
    <p>No comments found.</p>
@endforelse
```

---

### **4. Including Other Views**

#### **`@include` Directive**
Embeds another Blade view.
```php
@include('partials.header')
```

#### **`@includeIf` Directive**
Includes the view only if it exists.
```php
@includeIf('partials.sidebar')
```

#### **`@each` Directive**
Used for including a view for each item in a collection.
```php
@each('partials.comment', $comments, 'comment', 'partials.no-comments')
```

---

### **5. Components and Slots**
Blade allows you to create reusable components.

#### **Creating a Component**
1. Create a Blade file in `resources/views/components`.
   Example: `resources/views/components/alert.blade.php`
   ```php
   <div class="alert alert-{{ $type }}">
       {{ $slot }}
   </div>
   ```

2. Use it in a view:
   ```php
   <x-alert type="success">
       Operation completed successfully!
   </x-alert>
   ```

---

### **6. CSRF Protection**
Blade provides a directive to generate a CSRF token field for forms.
```php
<form method="POST" action="/submit">
    @csrf
    <input type="text" name="name">
    <button type="submit">Submit</button>
</form>
```

---

### **7. Other Useful Directives**

- **`@auth`**: Checks if the user is authenticated.
  ```php
  @auth
      <p>Welcome back, {{ auth()->user()->name }}</p>
  @endauth
  ```

- **`@guest`**: Checks if the user is not authenticated.
  ```php
  @guest
      <p>Please log in to continue.</p>
  @endguest
  ```

- **`@env`**: Runs content based on the application's environment.
  ```php
  @env('local')
      <p>You are in the local environment.</p>
  @endenv
  ```

- **`@push` and `@stack`**: Allow injecting content into specific sections of a layout.
  ```php
  @push('scripts')
      <script src="app.js"></script>
  @endpush
  ```

  In your layout:
  ```php
  @stack('scripts')
  ```

---

## **Key Points**
1. Blade directives simplify writing conditionals, loops, and other logic in views.
2. Directives like `@include` and `@component` make views reusable and modular.
3. Use CSRF tokens to secure your forms.
4. Blade escapes variables by default to prevent XSS vulnerabilities.

---

This tutorial provides a comprehensive guide to Blade directives, essential for creating clean and dynamic views in Laravel.
