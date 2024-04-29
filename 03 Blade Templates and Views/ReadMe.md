# Blade Templates

Laravel's Blade templating engine is a powerful tool for building dynamic and reusable views.
It provides a clean and expressive syntax for working with PHP code within your HTML templates.

```
Route::get('/', function () {
    return view('welcome', ['name' => 'John Doe']);
});
```

You may display the contents of the `name` variable like so:

```
Hello, {{ $name }}.
```

Blade's `{{ }}` echo statements are automatically sent through PHP's `htmlspecialchars` function to prevent XSS attacks.

# Blade Templates Basics

Blade templates use the `.blade.php` file extension and are located in the `resources/views` directory by default.
To create a Blade template, simply create a new `.blade.php` file in the views directory.

```
<html>
<head>
    <title>Welcome</title>
</head>
<body>
    <h1>Hello, {{ $name }}</h1>
</body>
</html>
```

# Blade Directives

Blade directives are special syntax provided by Laravel's Blade templating engine that allow you to embed PHP code directly into your views in a more concise and readable manner. Among these directives are the conditional directives `@if`, `@elseif`, `@else`, and `@endif`, which function similarly to their PHP counterparts.

```
@if (count($tasks) === 1)
   <h1>I have one task!</h1>
@elseif (count($tasks) > 1)
    <h1>I have multiple tasks!</h1>
@else
    <h1>I don't have any tasks!</h1>
@endif
```

in comparison on plain php:

```
<?php if(count($tasks) ===1){ ?>
     <h1>I have one task!</h1>
<?php } ?>
```

## Isset and Empty

Laravel's Blade templating engine provides two convenient directives,`@isset` and `@empty`, which offer shortcuts for common checks on variables.

- `@isset` directives

  ```
  @isset($tasks)
      // $tasks is defined and is not null...
  @endisset
  ```

  The `@isset` directive checks whether a variable is defined and not null. If `$tasks` is defined and not null, the code within the directive block will be executed.

- `@empty` directive

  ```
  @empty($tasks)
      // $tasks is "empty"...
  @endempty
  ```

  The `@empty` directive checks whether a variable is `"empty"` according to PHP's `empty()` function. An empty variable is one that is either `unset`, `null`, `false`, `0`, an empty string, or an empty array.

## Authentication Directives

Authentication directives in Laravel's Blade templating engine provide convenient shortcuts for checking whether a user is authenticated or is a guest (not authenticated). These directives, `@auth` and `@guest`, help streamline conditional logic related to user authentication in your views.

The `@auth` directive checks if the current user is authenticated. If the user is authenticated, meaning they are logged in, the code within the directive block will be executed.

```
@auth
    // The user is authenticated...
    // show this message if the user is authenticated
    <h1>Welcome to dashboard</h1>
@else
    // if the user is not authenticated
    <h1>Please login to use the dashboard</h1>
@endauth
```

The `@guest` directive checks if the current user is a guest, meaning they are not authenticated. If the user is a guest, the code within the directive block will be executed.

```
@guest
    // The user is a guest (not authenticated)...
@endguest
```

For instance, if you want to display login or registration options only to guests, you can place these within the `@guest` directive. This ensures that these options are only visible to users who are not logged in.

# Switch Directive

Switch statements can be constructed using the `@switch`, `@case`, `@break`, `@default` and `@endswitch` directives:

```
@switch($i)
    @case(1)
        First case...
        @break

    @case(2)
        Second case...
        @break

    @default
        Default case...
@endswitch
```

# Loops

In addition to conditional statements, Blade provides simple directives for working with PHP's loop structures. Again, each of these directives functions identically to their PHP counterparts:

```
@for ($i = 0; $i < 10; $i++)
    The current value is {{ $i }}
@endfor

@foreach ($users as $user)
    <p>This is user {{ $user->id }}</p>
@endforeach

@forelse ($users as $user)
    <li>{{ $user->name }}</li>
@empty
    <p>No users</p>
@endforelse

@while (true)
    <p>I'm looping forever.</p>
@endwhile
```

## Comments

Blade also allows you to define comments in your views. However, unlike HTML comments, Blade comments are not included in the HTML returned by your application:

```
{{-- This comment will not be present in the rendered HTML --}}
```

## Raw PHP

In some situations, it's useful to embed PHP code into your views. You can use the Blade @php directive to execute a block of plain PHP within your template:

```
@php
    $counter = 1;
@endphp
```

# Template inheritance

Template inheritance is a powerful feature in Laravel's Blade templating engine that allows you to create reusable layouts for your views. With template inheritance, you can define a master layout that contains the common structure of your web pages, and then extend and customize this layout in child views as needed.

Firstly, you create a master layout, often named something like `app.blade.php`, typically located in the `resources/views/layouts/` directory. This layout contains the common structure shared among multiple pages of your website.

```
<!-- app.blade.php -->

<!DOCTYPE html>
<html>
<head>
    <title>@yield("title")</title>
</head>
<body>
    @yield("content")
</body>
</html>
```

In this layout, we have placeholders defined using `@yield` directive. These placeholders, such as` @yield("title")` and `@yield("content")`, will be replaced by the content specified in the child views.

```
<!-- tasks.blade.php -->

@extends("layouts.app")

@section("title", "Task List")

@section("content")
    <h1>Sample Content</h1>
@endsection
```

In the child view, you define the content that should replace the placeholders defined in the master layout using `@section` directives. Here, `@section("title")` specifies the title of the webpage, and `@section("content")` specifies the main content of the webpage.

When you render the `tasks.blade.php` view, Laravel will automatically inject the title and content into the placeholders defined in the `app.blade.php` layout, resulting in a complete webpage with the specified layout and content.

## More on this topic?

[Blade Directives](https://laravel.com/docs/10.x/blade#introduction)
