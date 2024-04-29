# Form Request Validation

A Form Request in Laravel is a class that encapsulates the logic for validating incoming HTTP requests, typically form submissions. It allows you to centralize your validation logic and keep your controller methods clean and focused. Form Requests are often used to validate incoming data before it is processed by your application.

To create a form request class, you may use the make:request Artisan CLI command:

```
php artisan make:request TaskRequest
```

## Mass Assignment

You can perform mass assignment in Laravel. Mass assignment refers to the process of assigning an array of data to a model's attributes all at once.
It's a convenient way to quickly create or update model instances with multiple attributes.

## Using Mass Assignment:

Defining Fillable Attributes - In your Eloquent model class, you need to define which attributes are mass assignable by specifying them in the `$fillable` property. Only attributes listed in the `$fillable` property can be mass assigned.

Example:

```
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Task extends Model
{
    protected $fillable = ['title', 'description'];
}
```

## Creating a Model Instance

When creating a new model instance, you can pass an associative array containing the attribute names and values to the model's constructor or to the
`create()` method.

Example:

```
$incomingData = $request->validated();

// Using create() method
$task = Task::create([$incomingData]);
```

## Updating Model Attributes:

You can also use mass assignment to update existing model instances. Simply pass an associative array containing the attribute names and updated values to the `update()` method.

Example:

```
$incomingData = $request->validated();
$task = Task::updated([$incomingData]);
```
