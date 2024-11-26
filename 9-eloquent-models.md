
# Laravel Tutorial for Beginners: #9 - Eloquent Models

---

## **What are Eloquent Models?**
Eloquent is Laravel's Object-Relational Mapping (ORM) system, which simplifies database interactions by using models. Each Eloquent model corresponds to a database table, allowing you to perform CRUD (Create, Read, Update, Delete) operations using PHP code instead of raw SQL queries.

---

## **Step 1: Creating a Model**

### **1. Generate a Model**
Use the Artisan command to create a new Eloquent model:
```bash
php artisan make:model Post
```

This creates a `Post` model in the `app/Models` directory:
```php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    use HasFactory;
}
```

### **2. Generate a Model with a Migration**
To create a model along with a migration file, use:
```bash
php artisan make:model Post -m
```
This generates:
- `app/Models/Post.php` (the model).
- `database/migrations/{timestamp}_create_posts_table.php` (the migration file).

---

## **Step 2: Defining the Model**

### **1. Specifying the Table Name**
If the table name does not follow Laravel's naming convention (plural of the model name), specify the table explicitly:
```php
protected $table = 'blog_posts';
```

### **2. Primary Key**
If the primary key is not `id`, define it:
```php
protected $primaryKey = 'post_id';
```

### **3. Disable Auto-Increment**
If the primary key is not auto-incrementing, disable it:
```php
public $incrementing = false;
```

### **4. Timestamps**
To disable the `created_at` and `updated_at` timestamps:
```php
public $timestamps = false;
```

---

## **Step 3: Basic CRUD Operations**

### **1. Create a Record**
```php
use App\Models\Post;

$post = new Post();
$post->title = 'My First Post';
$post->content = 'This is the content of my first post.';
$post->save();
```

Or use `create()` with mass assignment:
```php
Post::create([
    'title' => 'My First Post',
    'content' => 'This is the content of my first post.',
]);
```
> Ensure the `$fillable` property is defined for mass assignment:
```php
protected $fillable = ['title', 'content'];
```

### **2. Retrieve Records**

- **Retrieve All Records**
  ```php
  $posts = Post::all();
  ```

- **Retrieve by ID**
  ```php
  $post = Post::find(1);
  ```

- **Retrieve with Conditions**
  ```php
  $posts = Post::where('status', 'published')->get();
  ```

### **3. Update a Record**
```php
$post = Post::find(1);
$post->title = 'Updated Title';
$post->save();
```

Or use `update()`:
```php
Post::where('id', 1)->update(['title' => 'Updated Title']);
```

### **4. Delete a Record**
```php
$post = Post::find(1);
$post->delete();
```

Or use `destroy()`:
```php
Post::destroy(1);
```

---

## **Step 4: Relationships**

### **1. One-to-One**
Define a one-to-one relationship:
```php
public function profile()
{
    return $this->hasOne(Profile::class);
}
```

Usage:
```php
$user = User::find(1);
$profile = $user->profile;
```

### **2. One-to-Many**
Define a one-to-many relationship:
```php
public function posts()
{
    return $this->hasMany(Post::class);
}
```

Usage:
```php
$user = User::find(1);
$posts = $user->posts;
```

### **3. Many-to-Many**
Define a many-to-many relationship:
```php
public function roles()
{
    return $this->belongsToMany(Role::class);
}
```

Usage:
```php
$user = User::find(1);
$roles = $user->roles;
```

---

## **Step 5: Query Scopes**

### **1. Local Scopes**
Define a reusable query in the model:
```php
public function scopePublished($query)
{
    return $query->where('status', 'published');
}
```

Usage:
```php
$posts = Post::published()->get();
```

### **2. Global Scopes**
Apply a condition to all queries for a model:
```php
protected static function booted()
{
    static::addGlobalScope('published', function ($query) {
        $query->where('status', 'published');
    });
}
```

---

## **Step 6: Eager Loading**

### **1. Loading Relationships**
Avoid N+1 query issues by eager loading related models:
```php
$users = User::with('posts')->get();
```

### **2. Nested Relationships**
Load nested relationships:
```php
$users = User::with('posts.comments')->get();
```

---

## **Step 7: Accessors and Mutators**

### **1. Accessors**
Modify attributes when retrieving them:
```php
public function getTitleAttribute($value)
{
    return ucfirst($value);
}
```

### **2. Mutators**
Modify attributes before saving them:
```php
public function setTitleAttribute($value)
{
    $this->attributes['title'] = strtolower($value);
}
```

---

## **Key Points**
1. Eloquent models simplify database interactions with an ORM.
2. Use relationships to manage associations between models.
3. Scopes and eager loading optimize query performance.
4. Accessors and mutators enable customization of attribute handling.

---

This tutorial provides a detailed guide to Eloquent Models in Laravel.
