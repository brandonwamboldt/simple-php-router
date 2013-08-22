Simple PHP Router
=================

[Original Blog Post](http://brandonwamboldt.ca/my-php-router-class-825/).

Recently I had some spare time and decided to rewrite the PHP Router I’ve been using on many of my recent projects. I prefer to have my projects setup with .htaccess which redirects all page requests to index.php which uses my router to decide which function to call. This approach allows me to write very clean, modular code.

My new router is very flexible, supports unit testing and can be extended. I’ve attached the source code to this post as well as an example of how to use it.

My new router requires PHP 5.3.0 for namespaces.

I took a lot of inspiration from the very popular framework called CodeIgniter among other projects I’ve worked on over the years.

Usage Example
-------------

```php
<?php
$router = new \Igniter\Router;

// Adding a basic route
$router->route('/login', 'login_function');

// Adding a route with a named alphanumeric capture, using the  syntax
$router->route('/user/view/<:username>', 'view_username');

// Adding a route with a named numeric capture, using the  syntax
$router->route('/user/view/<#user_id>', array('UserClass', 'view_user'));

// Adding a route with a wildcard capture (Including directory separtors), using
// the  syntax
$router->route('/browse/<*categories>', 'category_browse');

// Adding a wildcard capture (Excludes directory separators), using the
//  syntax
$router->route('/browse/<!category>', 'browse_category');

// Adding a custom regex capture using the  syntax
$router->route('/lookup/zipcode/<:zipcode|[0-9]{5}>', 'zipcode_func');

// Specifying priorities
$router->route('/users/all', 'view_users', 1); // Executes first
$router->route('/users/<:status>', 'view_users_by_status', 100); // Executes after

// Specifying a default callback function if no other route is matched
$router->default_route('page_404');

// Run the router
$router->execute()
```

License
-------

This code is available under the MIT license.