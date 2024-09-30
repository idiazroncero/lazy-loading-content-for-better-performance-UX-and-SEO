<div class="section-inner">

# Know your cache

</div>

|
|
|

<div class="section-inner">

## Do not put your LCP inside a placeholder

LCP Measures how quickly the page loads by looking<br>
at _when the largest element is rendered_.

**You want your LCP to be rendered as soon as possible**

If it's getting placeholdered, it can affect LCP score.

</div>

|
|
|

<div class="section-inner">

## Spot _cache smells_

`X-Drupal-Dynamic-Cache: UNCACHEABLE` is very strange:<br>
check for bubbling of tags, contexts or max-ages that should<br>
have been placeholdered instead.

`max-age: 0` should be your last resort<br>
even for placeholders.

A big ratio of `X-Drupal-Dynamic-Cache: MISS` means that<br>
some commonly invalidated tag or short max-age could be placeholdered.

</div>

|
|
|

<div class="section-inner">

## Adapt the auto placeholder conditions to your site

¿Is your site content-heavy, with frequent updates?<br>
Maybe placeholdering `node_list` tags is a good idea?

¿You only have a few, mainly admin users?<br>
Maybe you can safely remove the `user` context.

¿Is your webpage translated to a lot of languages?<br>
Consider adding the `languages` context.

</div>

|
|
|

<div class="section-inner">

## You might not need everything!

If your page serves only sesionless requests,<br>
**Page Cache** can be enough!

**Dynamic Page Cache** can serve both session and sessionless<br>
but will delegate session-less to **Page Cache**.

Under certain conditions, having **Dynamic Page Cache** serve also<br>
sesionless requests can be benefitial.

Optimize your strategy for your case.

</div>
