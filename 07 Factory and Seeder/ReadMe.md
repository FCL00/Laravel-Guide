# Fatory And Seeders

Database factories and seeders are essential tools in Laravel for populating your application's database with sample data.
Factories allow you to define the structure of your model instances,
while seeders enable you to generate and insert data into your database tables.

## Creating a Factory

You can generate a new factory using Artisan's make:factory command. Factories are typically stored in the database/factories directory and are used to define the structure of your model instances.

```
php artisan make:factory TaskFactory --model=Task
```

## Defining Model Factories

Within your factory class, you can use Faker to generate fake data for your model attributes.
Faker is a PHP library that provides a convenient way to generate random and realistic test data.

```
<?php
namespace Database\Factories;

use Illuminate\Database\Eloquent\Factories\Factory;
class TaskFactory extends Factory
{
    /**
     * Define the model's default state.
     *
     * @return array<string, mixed>
     */
    public function definition(): array
    {
        return [
            "title" => fake()->sentence(5),
            "description" => fake()->paragraph(1),
            "long_description" => fake()->paragraph(2, true),
            "complete" => fake()->boolean(50),
        ];
    }
}

```

# Running Seeders

You can execute your seeders to populate your database tables with sample data using the `db:seed` Artisan command.

```
php artisan db:seed
```
