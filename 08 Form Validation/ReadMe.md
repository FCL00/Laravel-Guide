# Form Validation

Form validation is a crucial aspect of web development, ensuring that data submitted through forms meets certain criteria or constraints before being processed by the server. In Laravel, form validation is made simple and efficient through its built-in validation features.

## Why Form Validation?

Form validation helps ensure data integrity and security by verifying that the data submitted by users is valid and meets the expected criteria. It prevents invalid or malicious data from being processed, reducing the risk of security vulnerabilities and data corruption.

## Laravel's Validation Features:

Laravel provides a comprehensive and expressive way to validate incoming form data. Key features include:

- Validation Rules - Laravel offers a wide range of validation rules to check various aspects of form data, such as required fields, data types, string lengths, email formats, and more.

- Error Messages - You can customize error messages for each validation rule, providing clear feedback to users about what went wrong when their input fails validation.

- Validation Requests - Laravel encourages separating validation logic from your controller methods by using Form Request validation classes. These classes contain validation rules and authorize methods, making your controller methods cleaner and more focused.

- Automatic Redirection - If form validation fails, Laravel automatically redirects the user back to the form with the validation errors flashed to the session, allowing you to display error messages alongside the form fields.

- Conditional Validation - You can conditionally apply validation rules based on other input or application logic, allowing for more complex validation scenarios.

# Performing Form Validation:

To perform form validation in Laravel, follow these general steps:

- Define Validation Rules - Specify validation rules for each form field in your application. You can define these rules directly in your controller methods or encapsulate them in separate Form Request classes.
- Validate Incoming Data - Use Laravel's validation features, such as the validate method or Form Request classes, to validate the incoming form data against the defined rules.
- Handle Validation Errors - If validation fails, Laravel automatically redirects the user back to the form with the validation errors flashed to the session. You can retrieve and display these error messages alongside the form fields to inform the user about what needs to be corrected.
- Process Valid Data - If validation passes, you can safely process the validated form data, knowing that it meets the specified criteria.

```
use Illuminate\Http\Request;
use App\Models\Post;

class PostController extends Controller
{
    public function store(Request $request)
    {
        $incomingData = $request->validate([
            "title" => "required|max:255",
            "description" => "required|max:255|min:2",
            "long_description" => "required|max:255"
        ]);
    }
}
```

All the data submitted through the form is available in the `$request` object.
Before storing this data, it's crucial to validate it to ensure it meets certain criteria.
We define validation rules for each input field to ensure the data is valid.

After validation, $incomingData contains only the validated input,
ensuring that it meets the specified rules and is safe to use.

Now you can proceed to store the validated data in your database, for example:

```
$task = new Task;
$task->title = strip_tags($incomingData["title"]);
$task->description = strip_tags($incomingData["description"]);
$task->long_description = strip_tags($incomingData["long_description"]);
$task->save();
```

Or using Mass Assignment

```
Task::create($incomingData);
```

Additionally, you can perform any necessary processing or manipulation of the data before storing it.
in the example below we are removing any HTML or PHP tags on the user so prevent XSS attacks.

```
$task->title = strip_tags($incomingData["title"]);
```

If validation fails, Laravel automatically redirects the user back to the form and display the errors.
The `@error` directive in Laravel's Blade templating engine is used to display validation error messages for a specific form field.
The `$message` variable contains the specific validation error message associated with the `"title"` field, as flashed to the session by Laravel.

```
<!-- this code snippet should be place inside your view pages -->
<form action="/your-route" method="POST">
    @csrf
    <label for="title">Title</label>
    <input type="text" id="title" name="title" placeholder="Enter your title" value="{{ old("title") }}" autocomplete="off" />

    <-- Displaying Validation Errors for the "title" field -->
    @error("title")
        <p class="text-red-500"> {{ $message }}</p>
    @enderror

    <button type="submit">Submit</button>
</form>

```

// with the validation errors flashed to the session, allowing for error messages to be displayed to the user.

// Handle the stored data or redirect the user to another page as needed.
