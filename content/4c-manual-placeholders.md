<div class="section-inner">

# Taking (consciuous)<br> control of placeholders

</div>

|
|
|

<div class="section-inner">

## We can opt-in to placeholdering

Most of the placeholdering is automatic<br>
and will take place inside Blocks.

We can nevertheless _decide_ when it's appropriate<br>
to enable placeholdering.

</div>
|
|
|

<div class="section-inner">

## Example: a controller with dynamic data

Let's imagine a _extremely static_ controller that<br>
returns content that won't change with an exception.

It renders a _random_ list of three nodes.<br>

It needs to renew the list each 3 minutes (`max-age: 180`)<br>
and depends on the `node_list` tag, which is problematic.

</div>

|
|
|

<div class="section-inner">

<div class="placeholder-sample font-xs">

<div class="placeholder-sample-static">
Can be cached infinitely
</div>

<div class="placeholder-sample-dynamic">

`max-age 180` / depends on `node_list`

  <div>
  <span></span>  <span></span>  <span></span>
  </div>
</div>

<div class="placeholder-sample-static">

Depends on a global, static cache tag such as `config:system.site`

</div>

</div>

</div>

|
|
|

<div class="section-inner">

### Opting in to placeholdering

```php[2-4|5-17|19-22|13]
$build = [
  'static-1' => [
    '#markup' => 'A lot of static text, render arrays and whatever'
  ]

  'dynamic' => [
    '#lazy_builder' => [self::class . '::lazyBuilder', []]
    '#lazy_builder_preview' => [
      ...
    ],
    '#create_placeholder' => TRUE,
    '#cache' => [
      'keys' => ['random-content-sample'],
      'max-age' => 180,
      'tags' => ['node_list']
    ]
  ]

  'static-2' => [
    '#markup' => 'More static content, with no dependencies
      or rather static dependencies such as { site_name }'
  ]
]
```

|
|
|

<div class="section-inner">

## Do not forget the cache keys!

When manually creating placeholders, it is usually<br>
needed to create a cache `key`.

It might need to be custom, as we are caching<br>
something Drupal is unaware of.

This ensures the result will be stored on the<br>
`render_cache` database and retrieved.

</div>
