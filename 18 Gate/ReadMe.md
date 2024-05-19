# Gate

what is gate exactly? Well, Laravel provides a powerful and flexible authorization system through Gates and Policies. Gates are simple, closure-based checks that determine whether a user is authorized to perform a given action, whereas Policies are classes that group authorization logic around a particular model or resource.

## Defining Gates

Gates are typically defined in the `AuthServiceProvider` class.
In this example we define a Gate to determin if a user is an admin and therefore allowed to visit the admin pages.

- Step 1: In the `AuthServiceProvider` class, we can register the Gate using the `Gate::define` method:

```
namespace App\Providers;

use Illuminate\Support\Facades\Gate;
use App\Models\User;
use Illuminate\Foundation\Support\Providers\AuthServiceProvider as ServiceProvider;

class AuthServiceProvider extends ServiceProvider
{
    protected $policies = [
        // Your model to policy mappings
    ];

    public function boot(): void
    {
        $this->registerPolicies();

        // Define the 'visitAdminPages' gate
        Gate::define('visitAdminPages', function(User $user) {
            return $user->isAdmin === 1;
        });
    }
}
```

`Note:` by default laravel will import Gate class for you however it was commented in the very top of the `AuthServiceProvider` class so
make sure to uncomment it when you are using Gate.

```
use Illuminate\Support\Facades\Gate; // uncomment this on the very top to use gate
```

# Using Gates in Controllers

We can use `Gates` directly in your controllers to authorize actions. Here’s how we can use the `visitAdminPages` Gate in the index method of our `AdminController`:

```
public function index()
{
    // Using the Gate in a controller
    if (Gate::allows('visitAdminPages')) {
        return "Only admin can access this page";
    }
    // if the user is not admin we redirect them back to home page
    return redirect()->route("user.home")->with("error", "You cannot access this page");
}
```

`Note:` in this example we are checking if the user is allows to visit the admin pages

# Using Gates in Routes with Middleware

Alternatively, you can use `Gates` in your `routes` by leveraging `middleware`.
Laravel’s `can` middleware provides a convenient way to apply `Gates` to `routes`.

- Step 1: Apply Middleware to Route
  In your `web.php` routes file, apply the `can` middleware to the route that should be restricted

```
Route::get('/admin-only', [AdminController::class, 'index'])->name('admin.index')->middleware('can:visitAdminPages');
```

`Note:` This middleware ensures that only users authorized by the `visitAdminPages` Gate can access the `/admin-only` route. If the user is not authorized, a `403 Forbidden` response is returned by default.
