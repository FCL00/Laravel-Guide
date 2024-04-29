## What is Laravel?

Laravel is an open-source PHP framework designed for building web applications following the MVC (Model-View-Controller) architectural pattern. Developed by Taylor Otwell in 2011, Laravel has gained immense popularity in the web development community due to its elegant syntax, developer-friendly features, and robust ecosystem.

## Installation

1. Firstly you need to install `XAMPP` because this application will already automatically download the `PHP` for you to use. but if you want to donwload the `PHP` seperately you follow this link to download it: [Download PHP latest version here](https://www.php.net/downloads.php) and watch this tutorial to install PHP properly: [Video](https://www.youtube.com/watch?v=MPRLUd8Pmyo)

   - [XAMPP](https://www.apachefriends.org/download.html)
   - [Composer](https://getcomposer.org/download/)
   - [PHP 8](https://www.php.net/downloads.php)

2. then after you install `XAMPP` you need to install [Composer](https://getcomposer.org/download/), Composer is a dependency manager for PHP that Laravel utilizes for managing its dependencies. Install Composer by following the instructions on the Composer website.

3. Once Composer is installed, you can create a new Laravel project using Composer's `create-project` command:

   Install laravel and create a new folder:

   ```
   composer create-project laravel/laravel your-project-name
   ```

   Or install laravel on existing folder

   ```
   composer create-project laravel/laravel .
   ```

   If you want to download laravel specific version:

   ```
   composer create-project laravel/laravel:^10 your-project-name
   ```

4. Run the Development Server: Navigate to your project directory and start the development server by running the following command:
   ```
   php artisan serve
   ```
   This will start a development server, and you can access your Laravel application by visiting `http://localhost:8000` in your web browser.
