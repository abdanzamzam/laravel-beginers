
# Laravel Tutorial for Beginners: #20 - Showing Form Errors

---

## **Introduction**
Displaying error messages for invalid form inputs is a crucial part of creating a user-friendly application. Laravel provides built-in tools to validate form inputs and display error messages seamlessly.

---

## **Step 1: Setting Up Validation in the Controller**

Define validation rules in the controller method handling the form submission. Use the `validate` method to automatically validate the incoming request data.

### **Example**
```php
namespace App\Http\Controllers;

use Illuminate\Http\Request;

class FormController extends Controller
{
    public function store(Request $request)
    {
        $validated = $request->validate([
            'name' => 'required|string|max:255',
            'email' => 'required|email',
            'message' => 'required|min:10',
        ]);

        // Logic to handle the validated data
        return back()->with('success', 'Form submitted successfully!');
    }
}
```

---

## **Step 2: Adding Error Messages to the View**

In your Blade view, you can use the `@error` directive to display validation error messages.

### **Example**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Form with Errors</title>
</head>
<body>
    <h1>Submit Your Details</h1>

    <!-- Display success message -->
    @if (session('success'))
        <p style="color: green;">{{ session('success') }}</p>
    @endif

    <!-- Form -->
    <form action="{{ route('form.store') }}" method="POST">
        @csrf

        <label for="name">Name:</label>
        <input type="text" id="name" name="name" value="{{ old('name') }}">
        @error('name')
            <p style="color: red;">{{ $message }}</p>
        @enderror
        <br><br>

        <label for="email">Email:</label>
        <input type="email" id="email" name="email" value="{{ old('email') }}">
        @error('email')
            <p style="color: red;">{{ $message }}</p>
        @enderror
        <br><br>

        <label for="message">Message:</label>
        <textarea id="message" name="message">{{ old('message') }}</textarea>
        @error('message')
            <p style="color: red;">{{ $message }}</p>
        @enderror
        <br><br>

        <button type="submit">Submit</button>
    </form>
</body>
</html>
```

---

## **Step 3: Highlighting Fields with Errors**

You can highlight input fields with errors by adding conditional CSS classes based on the presence of errors.

### **Example**
```html
<input type="text" id="name" name="name" class="{{ $errors->has('name') ? 'border-red' : '' }}" value="{{ old('name') }}">
```

Add a CSS class to style the error state:
```css
<style>
    .border-red {
        border: 1px solid red;
    }
</style>
```

---

## **Step 4: Displaying All Errors**

If you want to display all validation errors at once, use the `any` method to check for errors and the `$errors->all()` method to iterate over them.

### **Example**
```html
@if ($errors->any())
    <ul style="color: red;">
        @foreach ($errors->all() as $error)
            <li>{{ $error }}</li>
        @endforeach
    </ul>
@endif
```

---

## **Step 5: Customizing Error Messages**

You can customize validation error messages by passing a second parameter to the `validate` method.

### **Example**
```php
$request->validate([
    'name' => 'required|max:255',
    'email' => 'required|email',
    'message' => 'required|min:10',
], [
    'name.required' => 'The name field is mandatory.',
    'email.required' => 'Please provide a valid email address.',
    'message.required' => 'The message field cannot be empty.',
]);
```

---

## **Step 6: Using Translations for Error Messages**

Laravel supports translations for error messages. Define custom messages in `resources/lang/{locale}/validation.php`.

### **Example**
```php
// resources/lang/en/validation.php
return [
    'custom' => [
        'name' => [
            'required' => 'The name field is required.',
        ],
    ],
];
```

---

## **Step 7: Redirecting Back with Old Input**

Use `back()` with `withInput()` to redirect back to the form and retain old input values:
```php
return back()->withErrors($validator)->withInput();
```

In the Blade view, use `old()` to repopulate input fields:
```html
<input type="text" id="name" name="name" value="{{ old('name') }}">
```

---

## **Best Practices**

1. **Use the `@error` Directive**: It's simple and clean for displaying error messages.
2. **Display All Errors Clearly**: Use `any` and `all` methods for global error displays.
3. **Highlight Invalid Fields**: Use conditional CSS classes for better user experience.
4. **Customize Error Messages**: Provide meaningful and user-friendly error messages.
5. **Repopulate Fields**: Always repopulate fields with `old()` to improve usability.

---

## **Key Points**

1. Laravel provides the `validate` method to enforce input validation.
2. Use the `@error` directive to display individual error messages.
3. Customize error messages in the controller or `validation.php` files.
4. Highlight fields with errors for better user experience.

---

This tutorial provides a comprehensive guide to handling and displaying form errors in Laravel.
