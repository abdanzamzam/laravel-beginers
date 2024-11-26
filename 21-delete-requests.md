
# Laravel Tutorial for Beginners: #21 - Handling Delete Requests

---

## **Introduction**
Delete requests are used to remove data from a database. In Laravel, handling delete requests is straightforward and secure, thanks to features like route model binding and CSRF protection.

---

## **Step 1: Setting Up a Route**

Define a route to handle delete requests in `routes/web.php`:
```php
use App\Http\Controllers\DeleteRequestController;

Route::delete('/delete/{id}', [DeleteRequestController::class, 'destroy'])->name('delete');
```

---

## **Step 2: Creating the Controller**

Generate a controller to handle the delete request:
```bash
php artisan make:controller DeleteRequestController
```

In `DeleteRequestController`:
```php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Item; // Replace with your model

class DeleteRequestController extends Controller
{
    public function destroy($id)
    {
        $item = Item::findOrFail($id); // Find the item or throw a 404 error
        $item->delete(); // Delete the item

        return redirect()->back()->with('success', 'Item deleted successfully!');
    }
}
```

---

## **Step 3: Adding a Delete Button in the View**

Create a delete button in your Blade template. Use a form with the `DELETE` method and include the CSRF token for protection.

### **Example**
```html
@foreach ($items as $item)
    <div>
        <p>{{ $item->name }}</p>
        <form action="{{ route('delete', $item->id) }}" method="POST">
            @csrf
            @method('DELETE')
            <button type="submit">Delete</button>
        </form>
    </div>
@endforeach
```

---

## **Step 4: Protecting Delete Requests with CSRF**

Laravel requires a CSRF token for delete requests. Include `@csrf` in your form to generate a token automatically.

### **Why CSRF Protection is Important**
CSRF tokens ensure that delete requests are initiated from your application and not by malicious actors.

---

## **Step 5: Using Route Model Binding**

Simplify the process by using Laravel’s route model binding to automatically inject the model instance.

### **Route Definition**
```php
Route::delete('/delete/{item}', [DeleteRequestController::class, 'destroy'])->name('delete');
```

### **Controller Method**
```php
public function destroy(Item $item)
{
    $item->delete();

    return redirect()->back()->with('success', 'Item deleted successfully!');
}
```

With route model binding, Laravel automatically fetches the `Item` model based on the `{item}` parameter.

---

## **Step 6: Handling Soft Deletes**

If you want to preserve deleted records for future reference, enable soft deletes in your model.

### **Enable Soft Deletes**
1. Add the `SoftDeletes` trait to your model:
   ```php
   namespace App\Models;

   use Illuminate\Database\Eloquent\Model;
   use Illuminate\Database\Eloquent\SoftDeletes;

   class Item extends Model
   {
       use SoftDeletes;
   }
   ```

2. Update your migration to include a `deleted_at` column:
   ```php
   $table->softDeletes();
   ```

3. Use the `forceDelete` method to permanently delete records:
   ```php
   $item->forceDelete();
   ```

---

## **Step 7: Testing Delete Requests**

### **1. Manual Testing**
- Add an item to the database.
- Visit the page with the delete button.
- Click the button and verify the item is deleted.

### **2. Testing with Postman**
- Set the request type to `DELETE`.
- Provide the correct URL and ID.
- Include a valid CSRF token in the headers if required.

---

## **Best Practices**

1. **Use Route Model Binding**: Simplifies controller logic and ensures proper data handling.
2. **Implement CSRF Protection**: Always secure your forms with CSRF tokens.
3. **Use Soft Deletes**: Retain deleted data when necessary for auditing or recovery.
4. **Validate User Permissions**: Ensure only authorized users can delete records.

---

## **Key Points**

1. Use the `Route::delete` method to define delete routes.
2. Include `@csrf` and `@method('DELETE')` in forms to secure delete requests.
3. Use soft deletes to preserve data for recovery or auditing purposes.
4. Leverage route model binding for cleaner and more secure code.

---

This tutorial provides a comprehensive guide to handling delete requests in Laravel.
