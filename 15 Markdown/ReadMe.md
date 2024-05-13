## Markdown Support in Laravel

Laravel provides built-in support for Markdown through the `Str::markdown()` method, allowing developers to parse Markdown content and render it as HTML. Let's take a closer look at how we can utilize this feature in a Laravel application:

```
public function show(Post $post){
    // Markdown support
    // Allows users to format their blog post

    // Parse Markdown content
    $post["description"] = Str::markdown($post["description"]);

    // Pass the parsed Markdown content to the view
    return view('post.show', ['post' => $post]);
}
```

## Filter HTML tags to be rendered

To allow only certain HTML tags to be used while filtering out others, you can combine
`strip_tags()` with the `$allowed_tags` parameter.
This parameter specifies which tags are allowed to remain in the string,
while all other tags are removed. Here's how you can use `strip_tags()` to allow only specific HTML tags:

```
public function show(Post $post){
    // Allowed HTML tags
    $allowed_tags = '<p><a><ul><ol><li><strong><em><img><h1><h2><h3><h4><h5><h6>';

    // Strip disallowed tags and attributes, keeping only allowed tags
    $post["description"] = strip_tags($post["description"], $allowed_tags);

    // Parse Markdown content
    $post["description"] = Str::markdown($post["description"]);

    // Pass the sanitized and parsed Markdown content to the view
    return view('post.show', ['post' => $post]);
}
```

In the example above, `$allowed_tags` contains a list of HTML tags that you want to allow. When `strip_tags()` is called with this list as the second argument, it will remove any tags and attributes that are not included in the list. This ensures that only the specified tags remain in the content.

## Integrating Markdown in Views

Once the Markdown content is parsed, it can be seamlessly integrated into views using Laravel's Blade templating engine. Simply echo the parsed Markdown content within your Blade template to render it as HTML:

```
<div class="post-content">
    {!! $post->description !!}
</div>
```

Add this on your `post.show` page ` {!! $post->description !!}` or in your view page
This will tell Laravel that you don't need protection and we want to render the post as an HTML tag

## Benefits of Markdown in Blogging

1. Simplicity:
   Markdown offers a simple and intuitive syntax for formatting text, making it easy for users to create well-structured content without the need for complex HTML tags.

2. Consistency:
   By standardizing the formatting syntax, Markdown ensures consistency in the appearance of blog posts across different platforms and devices.

3. Readability:
   Markdown's plain text format enhances readability, allowing users to focus on writing content without distraction.

4. Security:
   Laravel's Markdown support ensures that parsed Markdown content is sanitized, mitigating the risk of XSS attacks and other security vulnerabilities.
