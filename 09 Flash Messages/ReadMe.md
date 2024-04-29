# Flash Messages

In Laravel, flash messages are used to temporarily store messages in the session that can be displayed to the user on subsequent requests.
They are often used to provide feedback or notifications to the user after certain actions, such as form submissions, redirects, or other operations.

## Storing Flash Messages

To store a flash message in the session, you use the `with()` method when redirecting or returning a response. This method accepts the session key and the value of the flash message. For example:

In this example, `'success'` is the session key, and '`Task created successfully.`' is the flash message.

```
Route::get("/your-route", function(){
    return redirect()->route('home')->with('success', 'Task created successfully.');
});
```

## Access Flash Messages

Flash messages can be accessed in Blade views using the `session()` helper function or the Session facade. For example:

```
@if(session()->has('success'))
    <div class="alert alert-success">
        {{ session('success') }}
    </div>
@endif
```

This code checks if a flash message with the key 'success' exists in the session.

## Displaying Flash Messages

Flash messages are typically displayed to the user as feedback or notifications. They can indicate the success or failure of an operation, provide information about errors or warnings, or convey other relevant messages.

## Automatic Removal

Flash messages are automatically removed from the session after they are accessed once. This means that they are only displayed to the user on the next request and are then discarded from the session.
