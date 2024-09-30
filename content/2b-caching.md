<div class="section-inner">

# The problem with caching

</div>

|
|
|

<div class="section-inner">

### Problem 1: <br> it takes just a single _miss_<br> to invalidate the whole page!

<div class="col-2">

<div class="col">

<img src="../images/miss.png" />

</div>

<div class="col">

If a single item on the page loses its cache,
all the page needs to be re-rendered

This has _heavy_ implications for performance if things change often.

Example: the `_list` cache tags<br> (`node_list`, `user_list`)

</div>

</div>

|
|
|

<div class="section-inner">

### Problem 2:<br> Some cache contexts have a _huge_ cardinality

A render array that shows the site name (no contexts)<br>
has just a single dependency (the site name config)<br>
and no contexts (it’s global).

A contextual render array like `{{ user_name }}` will have<br>
_as many possible variations as users_

If your page has tens of thousands of users,<br>
this can become a problem.

</div>

|
|
|

<div class="section-inner">

#### Cache contexts can grow exponentially!

You don't need a site with thousands of users<br>
to experience high levels of variation.

```php
$message = [
  '#markup' => "Welcome {user}! You are using the {theme} theme."
  '#cache' => [
    'contexts' => ['user', 'theme']
  ]
]
```

<div class="font-sm">

· It needs a cache entry for each possible combination of user and theme.<br>
· It needs to be invalidated on each user or theme change.

</div>

</div>

|
|
|

<div class="section-inner">

### It’s easy to make your page<br> almost uncacheable

```php
$build = [
  '#markup' => 'Related content written by you: { contents }'
  '#cache' => [
    'tags' => ['node_list'],
    'contexts' => ['user', 'url.path']
  ]
]
```

· If your code depends on generic tags.<br>
· If there are several contexts.<br>
· On short `max-age` scenarios.

</div>

|
|
|

<div class="section-inner">

### The problem is deeply ingrained

`user`<br>
`url.path`<br>
`session`<br>
`timezone`<br>
`languages`<br>
`cookies`<br>

<div class="alert">

This means that _especially_ logged in users have a huge chance of being almost uncacheable and suffer from performance issues due to the large amount of interrelated contexts + easily invalidable cache tags.

</div>

</div>
