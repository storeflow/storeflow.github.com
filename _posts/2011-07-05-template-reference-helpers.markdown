---
layout: default
title: Template reference helpers
description: Template reference helpers
categories: templates
---

[&laquo; Back to reference index](http://support.storeflowhq.com/help/kb/templates/template-reference)

## Available text formatting helpers

* append
* capitalize
* downcase
* escape
* escape_once
* highlight
* newline\_to_br
* pluralize
* prepend
* remove
* remove_first
* replace
* replace_first
* size
* strip_html
* strip_newlines
* times
* translate
* truncate
* truncatewords
* upcase

## Available array helpers

* first
* join
* last
* map
* size
* sort

## Available numbers, money and date helpers

* date
* divided_by
* minus
* money
* money\_with_currency
* plus

## Available tag helpers

* img_tag
* script_tag
* stylesheet_tag

## Available URL helpers

* asset_url
* flag\_img_url
* link_to
* link\_to_cart
* link\_to_collection
* link\_to_currency
* link\_to_language
* link\_to_page
* link\_to_product
* product\_img_url

## Text formatting

### append

Adds text at the end of another text.

    {% raw %}
    {{ 'Hello' | append: ' world!' }}
    {% endraw %}

Results in:

`Hello world!`

### capitalize

Capitalizes the first letter in a given text.

    {% raw %}
    {{ 'hello world!' | capitalize }}
    {% endraw %}

Results in:

`Hello world!`
    
### downcase

Converts every letter in a given text to lower caps.

    {% raw %}
    {{ 'Hello World!' | downcase }}
    {% endraw %}

Results in:

`hello world!`
    
### escape

Enables you to put text within HTML tag properties. In this example we would like the title of a product to be added to the title property of a link tag. If the product title includes double quotes this could break the link tag, but by using escape the double quotes will be converted to safe characters.
    
    {% raw %}
    <a href="{{ product.url }}" title="{{ product.title | escape }}">{{ product.title }}</a>
    {% endraw %}

Results in:

`<a href="/products/a_better_world" title="A &quot;Better&quot; World">A "Better" World</a>`
    
### escape_once

Prevents a given text from being escaped twice. If the escaped text in the example above would be escaped again, the result would be that the ampersand character would be converted to yet another symbol.
    
    {% raw %}
    {{ 'A &quot;Better&quot; World' | escape }}
    {% endraw %}

Results in:

`A &amp;quot;Better&amp;quot; World`

But by using escape_once all the characters that were escaped before will not be escaped again.

    {% raw %}
    {{ 'A &quot;Better&quot; World' | escape_once }}
    {% endraw %}

Results in:

`A &quot;Better&quot; World`

### highlight

Highlights specific words in a given text by wrapping an HTML element around them, which you can then style with CSS.

    {% raw %}
    {{ 'To be or not to be!' | highlight: 'be' }}
    {% endraw %}
    
Results in:

`To <strong class="highlight">be</strong> or not to <strong class="highlight">be</strong>!`

### newline\_to_br

Converts all line breaks to HTML &lt;br /&gt; tags.

    {% raw %}
    {{ 'Line 1
    Line 2
    Line 3'.newline_to_br }}
    {% endraw %}

Results in:

`Line 1<br /> Line 2<br /> Line 3<br />`

### pluralize

Returns a given text in either singular or plural form depending on the number provided.
    
    {% raw %}
    Hello {{ 3 | pluralize: 'world', 'worlds' }}!
    {% endraw %}

Results in:

`Hello worlds!`

You can also translate the result of this function, if a translation exists.

    {% raw %}
    Spanish: {{ 3 | pluralize: 'Product', 'Products' | translate }}
    {% endraw %}

Results in:

`Spanish: Productos`

### prepend

Adds text at the beginning of another text.

    {% raw %}
    {{ 'world!' | prepend: 'Hello ' }}
    {% endraw %}
    
Results in:

`Hello world!`
    
### remove

Removes the contents of a given text.

    {% raw %}
    {{ 'To be or not to be!' | remove: 'be' }}
    {% endraw %}

Results in:

`To or not to !`

### remove_first

Removes only the first occurrence of the contents of a given text.

    {% raw %}
    {{ 'To be or not to be!' | remove: 'be' }}
    {% endraw %}

Results in:

`To or not to be!`

### replace

Replaces the contents of a given text.

    {% raw %}
    {{ 'To be or not to be!' | replace: 'be', 'replace' }}
    {% endraw %}

Results in:

`To replace or not to replace!`

### replace_first

Replaces only the first occurrence of the contents of a given text.

    {% raw %}
    {{ 'To be or not to be!' | replace: 'be', 'replace' }}
    {% endraw %}

Results in:

`To replace or not to be!`

### size

Returns the number of characters in a given text.

    {% raw %}
    {{ 'Hello world!' | size }}
    {% endraw %}

Results in:

`12`

### strip_html

Removes HTML tags completely from a given text.

    {% raw %}
    {{ '<p>Hello <strong>world!</strong></p>'.strip_html }}
    {% endraw %}

Results in:

`Hello world!`

### strip_newlines

Removes all line breaks from a given text.

    {% raw %}
    {{ 'Line 1
    Line 2
    Line 3'.strip_newlines }}
    {% endraw %}

Results in:

`Line 1 Line 2 Line 3`

### times

Copies a given text a specific number of times.

    {% raw %}
    {{ 'Hello world!' | times: 3 }}
    {% endraw %}

Results in:

`Hello world!Hello world!Hello world!`

### translate

Translates a specific word into the currently selected language of your store. If a customer chooses to see your site in Spanish, the translation will be done automatically for you, as long as the word is defined in the language settings of your site.

    {% raw %}
    {{ 'hello_world' | translate }}
    {% endraw %}

Results in:

`Hola mundo!`

Remember, you can't translate something that hasn't been defined in your language settings. However, if a system translation isn't available you can add as many custom translations as you wish.

### truncate

Shortens a given text to a specific number of characters and adds '...' at the end, which you will need to take into account when specifying the number of characters.

    {% raw %}
    {{ 'Hello world!' | truncate: 8 }}
    {% endraw %}

Results in:

`Hello...`

### truncatewords

Shortens a given text to a specific number of words and adds '...' at the end.

    {% raw %}
    {{ 'To be or not to be!' | truncatewords: 4 }}
    {% endraw %}

Results in:

`To be or not...`

### upcase

Converts every letter in a given text to lower caps.

    {% raw %}
    {{ 'Hello world!' | upcase }}
    {% endraw %}

Results in:

`HELLO WORLD!`
    
## Arrays (list of objects)

### first

Finds the first item in an array.

    {% raw %}
    {{ site.currencies.first.title }}
    {% endraw %}

Results in:

`AUD`

### join

Joins every item in an array and returns them in a list. You can specify a separator, which will appear between each item. This method works best when the **map helper** is applied.

    {% raw %}
    {{ site.currencies | map: 'code' | join: ', ' }}
    {% endraw %}

Results in:

`AUD, USD, ZAR`

### last

Finds the last item in an array.

    {% raw %}
    {{ site.currencies.last.title }}
    {% endraw %}

Results in:

`ZAR`

### map

Joins every item in an array and returns a specific property of each item.

    {% raw %}
    {{ site.currencies | map: 'code' }}
    {% endraw %}

Results in:

`AUDUSDZAR`

Obviously this result isn't very useful, but by applying other array helpers, such as **join**, we can make sense of it all.

    {% raw %}
    {{ site.currencies | map: 'code' | join: ', ' }}
    {% endraw %}

Results in:

`AUD, USD, ZAR`

### size

Returns the number of items in an array.

    {% raw %}
    {{ site.currencies.size }}
    {% endraw %}

Results in:

`3`

### sort

Sorts an array by a specific property.

    {% raw %}
    {% for currency in site.currencies | sort: 'code' %}
      {{ currency.code }} - {{ currency.name }}
    {% endfor %}
    {% endraw %}

Results in:

    AUD - Australian Dollar
    USD - United States Dollar
    ZAR - South African Rand

## Numbers, money and dates

### date

Formats date and time to the currently selected locale settings or to specific formatting options.
    
    {% raw %}
    {{ 'now' | date }}
    {% endraw %}

Results in:

`June 28, 2011 11:39`

You can format the date and time any way you want with the formatting options listed below.
    
    {% raw %}
    Product is expected to arrive on {{ product.coming_soon_expected_date | date: "%B %d, %Y (%A)" }}
    {% endraw %}

Results in:

`Product is expected to arrive on October 01, 2011 (Saturday)`

You can also type a date and then format it using the formatting options.

    {% raw %}
    Printed on {{ '1.10.2011' | date: "%B %d, %Y (%A)" }}
    {% endraw %}

Results in:

`Printed on October 01, 2011 (Saturday)`

Full list of options for formatting:

    %a - The abbreviated weekday name ("Sun")
    %A - The full weekday name ("Sunday")
    %b - The abbreviated month name ("Jan")
    %B - The full month name ("January"")
    %c - The preferred local date and time representation
    %d - Day of the month (01..31)
    %e - Day of the month without a leading zero (1..31)
    %H - Hour of the day, 24-hour clock (00..23)
    %I - Hour of the day, 12-hour clock (01..12)
    %j - Day of the year (001..366)
    %m - Month of the year (01..12)
    %M - Minute of the hour (00..59)
    %p - Meridian indicator ("AM"    or "PM")
    %S - Second of the minute (00..60)
    %U - Week number of the current year,
         starting with the first Sunday as the first
         day of the first week (00..53)
    %W - Week number of the current year,
         starting with the first Monday as the first
         day of the first week (00..53)
    %w - Day of the week (Sunday is 0, 0..6)
    %x - Preferred representation for the date alone, no time
    %X - Preferred representation for the time alone, no date
    %y - Year without a century (00..99)
    %Y - Year with century
    %Z - Time zone name
    %% - Literal "%" character

Check out [foragoodstrftime.com](http://www.foragoodstrftime.com/) if you want to try these formatting options.

### divided_by

Performs a division.
    
    {% raw %}
    {{ 100 | divided_by: 25 }}
    {% endraw %}

Results in:

`4`

### minus

Performs a subtraction.

    {% raw %}
    {{ 100 | minus: 25 }}
    {% endraw %}

Results in:

`75`

### money

Represents a number as an amount of money.

    {% raw %}
    Price without money formatting: {{ product.price }}
    Price with money formatting: {{ product.price | money }}
    {% endraw %}

Results in:

    Price without money formatting: 1099
    Price with money formatting: 10.99

You can also specify your own number but remember that the number should include the cents.

    {% raw %}
    {{ 1099 | money }}
    {% endraw %}

Results in:

`10.99`

You can also add the currency sign or name by using the **money_with_currency** function.

    {% raw %}
    Price: {{ product.price | money_with_currency }}
    {% endraw %}

Results in:

`Price: $10.99`

### money\_with_currency

Represents a number as an amount of money with a currency sign or name. The currency sign or name will be determined by which currency your customer has selected on your store.

    {% raw %}
    Price without money formatting: {{ product.price }}
    Price with money formatting: {{ product.price | money_with_currency }}
    {% endraw %}

Results in:

    Price without money formatting: 1099
    Price with money formatting: $10.99

You can also specify the currency manually.

    {% raw %}
    Price: {{ product.price | money_with_currency: 'EUR' }}
    {% endraw %}

Results in:

`Price: €10.99`

### plus

Performs an addition.

    {% raw %}
    {{ 100 | plus: 25 }}
    {% endraw %}

Results in:

`125`

### times

Performs a multiplication.

    {% raw %}
    {{ 100 | times: 25 }}
    {% endraw %}

Results in:

`2500`

## Tags

### img_tag

Returns an HTML &lt;img&gt; tag for displaying an image. Usually chained with the asset_url function to ensure that the image is being fetched from the assets folder in your template. You can also specify an alt text.

    {% raw %}
    {{ 'image.png' | asset_url | img_tag: 'My Image' }}
    {% endraw %}

Results in:

`<img src="http://static.storeflowhq.com/assets/0000/0001/theme/image.png" alt="My Image" />`

### script_tag

Returns an HTML &lt;script&gt; tag for loading a Javascript file. Usually chained with the asset_url function to ensure that the Javascript file is being fetched from the assets folder in your template.

    {% raw %}
    {{ 'jquery.js' | asset_url | script_tag }}
    {% endraw %}

Results in:

`<script src="http://static.storeflowhq.com/assets/0000/0001/theme/jquery.js" type="text/javascript"></script>`

### stylesheet_tag

Returns an HTML &lt;link&gt; tag for loading a CSS file. Usually chained with the asset_url function to ensure that the CSS file is being fetched from the assets folder in your template.

    {% raw %}
    {{ 'style.css' | asset_url | stylesheet_tag }}
    {% endraw %}

Results in:

`<link href="http://static.storeflowhq.com/assets/0000/0001/theme/style.css" rel="stylesheet" type="text/css" media="all" />`

## URLs

### asset_url

Returns the full URL to your site's assets and enables to access all the assets in a simple way.

    {% raw %}
    {{ 'image.png' | asset_url }}
    {% endraw %}

Results in:

`http://static.storeflowhq.com/assets/0000/0001/theme/image.png`

You can also chain the URL with a tag function. In this example an &lt;img&gt; tag is being generated with an alt text.

    {% raw %}
    {{ 'image.png' | asset_url | img_tag: 'My Image' }}
    {% endraw %}

Results in:

`<img src="http://static.storeflowhq.com/assets/0000/0001/theme/image.png" alt="My Image" />`

### flag\_img_url

Returns the URL to an icon of the flag of a specific country.

    {% raw %}
    {{ 'us' | flag_img_url }}
    {% endraw %}

Results in:

`http://shared.storeflowhq.local/images/flags/small/us.png`

You can also specify the size of the flag (currently only 'small' and 'medium' are available) and chain the URL with the image tag.

    {% raw %}
    {{ 'uk' | flag_img_url: 'medium' | img_tag }}
    {% endraw %}

Results in:

`<img src="http://shared.storeflowhq.local/images/flags/medium/uk.png" />`

### link_to

Generates a link to a specific URL or object.

    {% raw %}
    {{ 'Go to StoreflowHQ.com' | link_to: 'http://www.storeflowhq.com' }}
    {% endraw %}

You can also link directly to an object, such as a collection, page, product, etc.

    {% raw %}
    {{ product | link_to }}
    {% endraw %}

Results in:

`<a href="http://demo.mystoreflow.com/en/products/storeflow-t-shirt">Storeflow T-shirt</a>`

You can link to an object using your own description:

    {% raw %}
    {{ 'View Product' | link_to: product }}
    {% endraw %}

Results in:

`<a href="http://demo.mystoreflow.com/en/products/storeflow-t-shirt">View Product</a>`

You can link to an object by its handle.

    {% raw %}
    {{ pages.about-us | link_to }}
    {% endraw %}

Results in:

`<a href="http://demo.mystoreflow.com/en/pages/about-us">About Us</a>`

Finally, you the option of a title property in all of the above cases.

    {% raw %}
    {{ 'Go to StoreflowHQ.com' | link_to: 'http://www.storeflowhq.com', 'Storeflow Website' }}
    {% endraw %}

Results in:

`<a href="http://www.storeflowhq.com" title="Storeflow Website">Go to StoreflowHQ.com</a>`

### link\_to_cart

Generates a link to the cart.

    {% raw %}
    {{ 'Go to Shopping Cart' | link_to_cart }}
    {% endraw %}

Also used to generate a link when adding a product to the cart.

    {% raw %}
    {{ 'Add to Cart' | link_to_cart: product }}
    {% endraw %}

Results in:

`<a href="/en/cart/add?product=1">Add to Cart</a>`

### link\_to_collection

Generates a link to a specific collection.
For the sake of simplicity, we recommend that you use the `link_to` tag when linking to a collection.

    {% raw %}
    {{ collection | link_to }}
    {% endraw %}

However, the advantage of this helper is that you can link to a collection by a string handle or integer ID.

    {% raw %}
    {{ 't-shirts' | link_to_collection }}
    {% endraw %}

### link\_to_currency

Generates a link to a specific currency.
For the sake of simplicity, we recommend that you use the `link_to` tag when linking to a currency.

    {% raw %}
    {{ currency | link_to }}
    {% endraw %}

However, the advantage of this helper is that you can link to a currency by its ISO code.

    {% raw %}
    {{ 'USD' | link_to_currency }}
    {% endraw %}

### link\_to_language

Generates a link to a specific language.
For the sake of simplicity, we recommend that you use the `link_to` tag when linking to a language.

    {% raw %}
    {{ language | link_to }}
    {% endraw %}

However, the advantage of this helper is that you can link to a language by its ISO code.

    {% raw %}
    {{ 'en' | link_to_language }}
    {% endraw %}

### link\_to_page

Generates a link to a specific page.
For the sake of simplicity, we recommend that you use the `link_to` tag when linking to a page.

    {% raw %}
    {{ page | link_to }}
    {% endraw %}

However, the advantage of this helper is that you can link to a page by a string handle or integer ID.

    {% raw %}
    {{ 'about-us' | link_to_page }}
    {% endraw %}

### link\_to_product

Generates a link to a specific product.
For the sake of simplicity, we recommend that you use the `link_to` tag when linking to a product.

    {% raw %}
    {{ product | link_to }}
    {% endraw %}

However, the advantage of this helper is that you can link to a product by a string handle or integer ID.

    {% raw %}
    {{ 'storeflow-t-shirt' | link_to_product }}
    {% endraw %}

### product\_img_url

Returns the URL to a specific product image. The image size can be defined.

    {% raw %}
    {{ product.images.first | product_img_url: 'thumb' }}
    {% endraw %}

Results in:

`<img src="http://static.storeflowhq.com/assets/0000/0001/images/thumb/storeflow_t_shirt.jpg" alt="Storeflow T-shirt" />`

Available product sizes (along with the maximum width and height in pixels):

    pico       16x16
    icon       32x32
    thumb      50x50
    small      100x100
    compact    160x160
    medium     240x240
    large      480x480
    xlarge     600x600
    original   1024x1024

## Back to Index

[&laquo; Back to reference index](http://support.storeflowhq.com/help/kb/templates/template-reference)