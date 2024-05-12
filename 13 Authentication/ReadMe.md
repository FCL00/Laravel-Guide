# Creating the UserController

In Laravel, controllers handle the application logic. Let's create a `UserController` to manage user-related actions such as `login`, `logout`, and `registration`.

command to create a `UserController`

```
php artisan make:controller UserController
```

sample boilerplate for `UserController`

```
namespace App\Http\Controllers;

use App\Models\User;
use Illuminate\Http\Request;
use Illuminate\Validation\Rule;
use Illuminate\Validation\Rules\Password;

class UserController extends Controller
{
    // Controller methods here
}
```

## Registration or Sign-Up

Create a method inside the `UserController` to show the registration form

```
 public function showRegistration(){
    return view('name of view for your form');
 }
```

Create registration method inside the `UserController`, this method will handle the post request of the user to create an account.
[Learn More about the Rules](#rule)

```
public function registration(Request $request){

    $incomingData = $request->validate([
        "username" => ["required", "min:3", "max:30", Rule::unique("users", "username")],
        "email" => ["required", "email", Rule::unique("users", "email")],
        "password" => ["required", "confirmed", Password::min(8)->mixedCase()->numbers()->symbols()],
    ]);

    User::create($incomingData);
    return redirect()->route("user.login")->with("success", "You have successfully registered");
}
```

## Login

The login() method in the UserController handles user login attempts:

```
public function login(Request $request){
    $incomingData = $request->validate([
        "username" => "required",
        "password" => "required"
    ]);

    // Attempting to login
    if( auth()->attempt(["username" => $incomingData["username"], "password" => $incomingData["password"]])){
        // If successful, regenerate session and redirect to dashboard
        $request->session()->regenerate();
        return redirect()->route("user.dashboard");
    }
    else{
        // Redirect back with error message
        return back()->with("error", "Incorrect Username or Password");
    }
}
```

In this example we use the `auth()->attempt()` to attempt to login using the user credentials provided by the user.

## Logout

The `logout()` method in the `UserController` logs out the user:

```
public function logout(){
    auth()->logout();
    return redirect()->route('user.loginPage')->with("success", "You have successfully logged out");
}
```

## Checking Authentication

To protect routes that require authentication, we can use the `auth()->check()` method.
Here's an example of how we can use it in a route definition:

```
Route::get('/dashboard', function () {
    if (auth()->check()) {
        // check if the User is authenticated
        return view('dashboard');
    } else {
        // if not Redirect the user to the login page
        return redirect('/login');
    }
});
```

## Note

`$request` is the variable that will be getting all data sent by the user and those data needs to be validated first before we even save it into another variable.

remember `$request` is a new instance of the `Request` class that means it inherent all the property and methods available inside the `Request` class. We are going to use the validate method to validate the incoming data and set the rules what kind of data is allowed to get in.

## Rule

The Rule class provides a fluent interface for defining custom validation rules. It allows developers to create rules that can be applied to validate various types of input data. In the context of user authentication, the Rule class is often used to define rules for validating unique fields, such as unique usernames or email addresses.

Note: make sure you import the Rule class before you even use it

```
use Illuminate\Validation\Rule;
use Illuminate\Validation\Rules\Password;
```

```
"username" => ["required", "min:3", "max:30", Rule::unique("users", "username")],
```

```
"email" => ["required", "email", Rule::unique("users", "email")],
```

in this example we use utility class called `Rule` because we want to check if the `username` provided by the user is already exist in our database if the `username` already exist then is not allowed because we need a unique `username` for every user and we also want the same `rule` with the `email`.

## Password

The Password class provides a fluent interface for defining rules for validating password strength. It allows developers to specify requirements for passwords, such as minimum length, mixed case characters, numbers, and symbols. This class is particularly useful when implementing password policies to enhance the security of user accounts.

```
"password" => ["required", "confirmed", Password::min(8)->mixedCase()->numbers()->symbols()]
```

In this example we want our `password` to be in mixedCase, lowercase and uppercase letters, it needs to have numbers and also symbols.
