# Laravel Assets

Place your JavaScript and CSS files in the public directory, which is directly accessible by the browser.
For example:

- `public/css` for your CSS files.
- `public/js` for your JavaScript files.

## Create Your CSS and JavaScript File

Place your JavaScript file in the `public/js` or `public/css` directory,
for example, `public/js/app.js` or `public/css/app.css`.
Add your custom JavaScript code or CSS Style to this file.

## Include Assets in Blade Templates

Now you can include your CSS and JavaScript files in your Blade templates.
Here’s an example of how to include these assets in your main layout file:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Laravel App</title>
    <link href="{{ asset('css/app.css') }}" rel="stylesheet">
</head>
<body>
    <h1>Welcome to My Laravel App</h1>

    <script src="{{ asset('js/app.js') }}"></script>
</body>
</html>
```

`Note:` In this example, `asset('css/app.css')` and `asset('js/app.js')`
generate the correct URLs to your CSS and JavaScript files in the public directory.

## Example Project Structure

Here’s a quick overview of how your project structure might look:

```
my-laravel-app/
├── public/
│   ├── css/
│   │   ├── app.css
│   │   └── tailwind.css
│   ├── js/
│   │   └── app.js
├── resources/
│   ├── views/
│   │   └── welcome.blade.php
├── tailwind.config.js
├── package.json
```

## Installing TailwindCSS

If you are using TailwindCSS, you need to install it and generate the configuration file. First, ensure you have `Node.js` and `npm` installed, then install `TailwindCSS`:

```
npm install tailwindcss
```

Next, generate the TailwindCSS configuration file:

```
npx tailwindcss init
```

You can configure your `TailwindCSS` settings in the generated `tailwind.config.js` file.

## Create Your CSS File with TailwindCSS

Create a CSS file where you will import TailwindCSS. For example, create

`public/css/tailwind.css` and add the following:

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Include Assets in Blade Templates

set up your `welcome.blade.php` or `app.blade.php` and other Blade templates to use Vite's `@vite` directive to load assets.
Ensure your Blade template includes the Vite directives to load your CSS and JavaScript:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Laravel App</title>
    @vite('resources/css/app.css')
</head>
<body>
    <h1>Welcome to My Laravel App</h1>
    @vite('resources/js/app.js')
</body>
</html>
```

## Compile Your Assets

Run the following command to start the Vite development server, which will watch your files and compile them as needed:

```
npm run dev
```

For production builds, use:

```
npm run build
```
