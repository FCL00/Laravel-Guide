# Route Model Binding

Route model binding is a technique used in Laravel to automatically inject model instances into controller methods based on route parameters.
Instead of manually fetching the model from the database using the route parameter, Laravel automatically resolves the model instance for you.

## Type Hinting

Type hinting is a PHP feature that allows you to specify the expected data type of a function or method parameter. In the context of Laravel controllers, type hinting is often used with route model binding to specify the expected model class for a route parameter.

## How it Works

1. Define Route Parameter - In your route definition, you specify a route parameter placeholder, typically `{model}`, that corresponds to the primary key of the model you want to bind.

2. Controller Method Signature - In your controller method, you type hint the parameter with the corresponding Eloquent model class. Laravel will automatically resolve the model instance based on the route parameter.

3. Automatic Injection - When the route is matched, Laravel automatically retrieves the model instance from the database using the route parameter value and injects it into the controller method.

Route:

```
Route::get('/task/edit/{task}', [TaskController:class, "edit"]);
```

Task Controller:

```
use App\Models\Post;

class TaskController extends Controller
{
    // Using type hinting with route model binding
    public function show(Task $task)
    {
        return view('task.show', ['task' => $task ]);
    }
}
```

`$task` is automatically resolved with the corresponding Task model instance
