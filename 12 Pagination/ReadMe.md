# Pagination

In Laravel, pagination allows you to split large sets of data into smaller, manageable chunks or pages, making it easier to navigate and display data in your application's views. Laravel provides convenient methods for paginating database query results.

## Using Pagination in Laravel

To paginate query results in Laravel, you can use the paginate() method, which is available on query builder instances and Eloquent model query builder instances.

```
// in your controller
$posts = Post::latest()->paginate(10);
```

```
// in your views
@foreach ($posts as $post)
    <!-- Display post details here -->
@endforeach

{{ $posts->links() }}
```

In this example, `paginate(10)` retrieves `10 records` per page from the tasks table using the Task model.

## Displaying Paginated Data in Views

To display paginated data in your views, you typically use the `links()` method provided by the paginator instance, which generates pagination links for navigating between pages.

## Pagination Not Working

[Pagination Not Working](https://stackoverflow.com/questions/65381519/pagination-not-showing-number-in-laravel-8)
