# Queries

Laravel Tinker is a powerful REPL (Read-Eval-Print Loop) that allows you to interact with your Laravel application from the command line. It provides a convenient way to test out Eloquent queries, relationships, and other parts of your application without needing to write and run scripts.

## How to use Tinker

To start using Tinker, you need to have Laravel installed and running. Open your terminal and run the following command from the root of your Laravel project:

```
php artisan tinker
```

`Note:` This will open the Tinker interactive shell, where you can start experimenting with your models and database.

## Examples of Eloquent Queries with Tinker

We have two models, `User` and `Post`, with the following relationships defined:

A User can have many `Post` models (`hasMany` relationship).

A `Post` belongs to a `User` (`belongsTo` relationship).

- In your `User` model (`app/Models/User.php`):

  ```
  public function posts()
  {
      return $this->hasMany(Post::class, 'user_id');
  }
  ```

- In your Post model (`app/Models/Post.php`):

  ```
  public function user()
  {
      return $this->belongsTo(User::class, 'user_id');
  }
  ```

## Basic Eloquent Queries

- Fetch all users
  ```
  // This retrieves all records from the users table.
  $users = App\Models\User::all();
  ```
- Fetch a user by ID
  ```
  // This retrieves the user with the specified ID. In this case, the user with ID 1.
  $user = App\Models\User::find(1);
  ```
- Fetch posts of the user
  ```
  // This retrieves all posts associated with the user fetched in the previous query.
  $posts = $user->posts;
  ```
- Fetch the user of a post
  ```
  // This retrieves the user who created the post with the specified ID. In this case, the post with ID 1.
  $post = App\Models\Post::find(1);
  $user = $post->user;
  ```
- Create a new user
  ```
  // This creates a new user record with the specified attributes.
  $newUser = App\Models\User::create([
      'name' => 'Jane Doe',
      'email' => 'jane@example.com',
      'password' => bcrypt('password'), // Password should be hashed
      'isAdmin' => 0
  ]);
  ```
- Create a post for the new user
  ```
  // This creates a new post associated with the user created in the previous query.
  $newPost = App\Models\Post::create([
      'title' => 'Jane\'s First Post',
      'description' => 'This is the description of Jane\'s first post.',
      'user_id' => $newUser->id // Associate the post with the newly created user
  ]);
  ```
- Update a user's name
  ```
  // This fetches the user with ID 1, updates their name, and saves the changes.
  $user = App\Models\User::find(1);
  $user->name = 'John Updated';
  $user->save();
  ```
- Delete a user
  ```
  // This fetches the user with ID 2 and deletes the record from the database.
  $userToDelete = App\Models\User::find(2);
  $userToDelete->delete();
  ```
- Fetch users with a specific condition
  ```
  // This retrieves all users who are administrators (isAdmin field is 1).
  $admins = App\Models\User::where('isAdmin', 1)->get();
  ```
- Fetch users and eager load their posts
  ```
  // This retrieves all users and their associated posts in a single query.
  $usersWithPosts = App\Models\User::with('posts')->get();
  ```
- Fetch a specific user and their posts
  ```
  // This fetches the user with ID 1 and eager loads their posts.
  $userWithPosts = App\Models\User::with('posts')->find(1);
  ```
- Fetch posts created by a specific user
  ```
  // This retrieves all posts where the user_id matches the specified ID. In this case, the user with ID 1.
  $userPosts = App\Models\Post::where('user_id', 1)->get();
  ```

## Advanced Eloquent Queries and Operations

- Fetch the first user
  ```
  // This retrieves the first user record in the users table based on the default order.
  $firstUser = App\Models\User::first();
  ```
- Fetch the last user
  ```
  // This retrieves the last user record in the users table based on the default order.
  $lastUser = App\Models\User::orderBy('id', 'desc')->first();
  ```
- Get a count of all users
  ```
  // This returns the total number of user records in the users table.
  $userCount = App\Models\User::count();
  ```
- Get a count of posts for a specific user

  ```
  // This returns the total number of posts created by the user with ID 1.
  $postCount = App\Models\Post::where('user_id', 1)->count();
  ```

- Fetch users with at least one post

  ```
  // This retrieves all users who have at least one associated post.
  $usersWithPosts = App\Models\User::has('posts')->get();
  ```

- Fetch users without any posts

  ```
  // This retrieves all users who do not have any associated posts.
  $usersWithoutPosts = App\Models.User::doesntHave('posts')->get();
  ```

- Fetch posts along with the user who created each post

  ```
  // This retrieves all posts and eager loads the user who created each post.
  $postsWithUsers = App\Models\Post::with('user')->get();
  ```

- Fetch the latest user

  ```
  // This retrieves the most recently created user record.
  $latestUser = App\Models\User::latest()->first();
  ```

- Fetch the latest 5 posts

  ```
  // This retrieves the 5 most recently created post records.
  $latestPosts = App\Models\Post::latest()->take(5)->get();
  ```

- Soft delete a user

  ```
  // This performs a soft delete on the user with ID 3, marking them as deleted without removing the record from the database.
  $user = App\Models\User::find(3);
  $user->delete(); // This requires the User model to use the SoftDeletes trait.
  ```

- Restore a soft deleted user
  ```
  // This restores a previously soft deleted user record.
  $user = App\Models\User::withTrashed()->find(3);
  $user->restore();
  ```
- Permanently delete a user

  ```
  // This permanently deletes the user with ID 3, removing the record from the database.
  $user = App\Models.User::withTrashed()->find(3);
  $user->forceDelete();
  ```

- Update multiple records

  ```
  // This updates all users, setting a default password (hashed) for each.
  App\Models\User::query()->update(['password' => bcrypt('defaultpassword')]);
  ```

- Create multiple posts for a user
  ```
  // This creates multiple posts for the user with ID 1.
  $user = App\Models.User::find(1);
  $user->posts()->createMany([
    ['title' => 'Post 1', 'description' => 'Description for post 1'],
    ['title' => 'Post 2', 'description' => 'Description for post 2'],
  ]);
  ```

# Laravel's Query Builder

Laravel's Query Builder provides a fluent interface for creating and running database queries. You can use Query Builder to perform CRUD operations, apply conditions, join tables, and more.

```
// Fetch all users using Query Builder
$users = DB::table('users')->get();
```

```
// Fetch a specific user by ID
$user = DB::table('users')->where('id', 1)->first();
```

```
// Fetch users with a specific condition
$activeUsers = DB::table('users')->where('is_active', 1)->get();
```

```
// Insert a new user record
$insertedUserId = DB::table('users')->insertGetId([
    'name' => 'John Doe',
    'email' => 'john@example.com',
    'password' => bcrypt('password'),
    'isAdmin' => 0,
]);
```

```
// Update a user's name
DB::table('users')->where('id', 1)->update(['name' => 'Updated Name']);
```

```
// Delete a user record
DB::table('users')->where('id', 2)->delete();
```

```
// Fetch posts along with the user who created each post using a join
$postsWithUsers = DB::table('posts')
    ->join('users', 'posts.user_id', '=', 'users.id')
    ->select('posts.*', 'users.name as user_name')
    ->get();
```

```
// Count the number of active users
$activeUserCount = DB::table('users')->where('is_active', 1)->count();
```
