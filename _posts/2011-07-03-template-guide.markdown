---
layout: default
title: Template guide
description: Template guide
categories: templates
---

## Introduction

Storeflow's powerful and flexible template engine allows you to customize the design of your store using HTML, CSS and a range of functions and variables.

The template engine provides the following:

* Logic functions
* Helpers
* Global variables
* Objects

[Click here to access the template reference.](http://support.storeflowhq.com/help/kb/templates/template-reference)

**This guide assumes you know HTML and CSS basics.**

## Files and Directories

Every theme is based around the same directory structure. A theme will have the following directories:

    assets
    config
    layouts
    snippets
    templates

* **assets** &mdash; Every CSS, Javascript, image or media file must be stored in this directory. This is the public directory of the theme.

* **config** &mdash; A theme will often have a set of settings that allow you to make certain changes to it in the administration panel. These settings are stored as a JSON object in a file called `settings.json`.

* **layouts** &mdash; A layout is all the HTML that is wrapped around your templates. A theme requires at least one layout file, usually called `theme.liquid`.

* **snippets** &mdash; Snippets are pieces of HTML and template code that you can include in your template files.

* **templates** &mdash; For each part of your store there is a corresponding template file. These are the required template files:

    404.liquid<br />
    cart.liquid<br />
    collection.liquid<br />
    index.liquid<br />
    page.liquid<br />
    product.liquid<br />
    search.liquid

## The Basics

A good way to start building a theme is to create the main layout file. So, let's create all the required directories (see above) and add a file called `theme.liquid` to the `layouts` directory. This is what a basic `theme.liquid` file might look like:

    {% raw %}
    <!DOCTYPE html>
    <html>
    <head>
      <title>{{ site.title }}</title>
      <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
      {{ 'style.css' | asset_url | stylesheet_tag }}
    </head>
    <body>
      <h1>{{ site.title }}</h1>

      {% for collection in collections %}
        <p><a href="{{ collection.path }}">{{ collection.title }}</a></p>
      {% endfor %}

      {{ content_for_layout }}

      <p>Copyright {{ site.title }} - {{ 'all_rights_reserved' | translate }}.</p>
    </body>
    </html>
    {% endraw %}

Notice the strange brackets and tags? This is how we get information from our store and place it into our templates. Let's break it down to smaller sections and get started on the fun stuff.

### Objects

The first thing you'll notice is the title tag:

    {% raw %}
    <title>{{ site.title }}</title>
    {% endraw %}

The template engine allows you to use objects. An object gives you information on a specific part of your store by using what's called properties. In this case `site` is an object and `title` is a property and when you combine the two into `site.title` you will get the title of your store that you defined in the administration panel.

You can get a lot more information about your store by using all the available objects. [Click here to read more about objects.](http://support.storeflowhq.com/help/kb/templates/objects)

### Helpers

So, on to the next part:

    {% raw %}
    {{ 'style.css' | asset_url | stylesheet_tag }}
    {% endraw %}

Another powerful feature of the template engine is the use of helpers. In this case we are sending the text `style.css` to the `asset_url` helper, which adds the theme's public directory to our stylesheet name:

    http://static.storecdn.com/assets/0000/0001/theme/style.css

Then we send THAT to the `stylesheet_tag` helper, which generates a complete &lt;link&gt; tag for our HTML:

    <link href="http://static.storecdn.com/assets/0000/0001/theme/style.css" rel="stylesheet" type="text/css" media="all" />

There are a lot of more helpers available. [Click here to read more about helpers.](http://support.storeflowhq.com/help/kb/templates/helpers)

### Logic Functions and Global Variables

This next part is a bit tricky:

    {% raw %}
    {% for collection in collections %}
      <p><a href="{{ collection.path }}">{{ collection.title }}</a></p>
    {% endfor %}
    {% endraw %}

When showing a list of objects, such as collections, you use a `for loop`. What a for loop does is go through each item in the list and show the HTML code that you provide. In this case we are showing a list of all the collections in our store and generating a link to the collection's page. Notice that we are using the properties `path` and `title` for each collection. This is the result of our for loop:

    <p><a href="/en/collections/womenswear">Womenswear</a></p>
    <p><a href="/en/collections/menswear">Menswear</a></p>
    <p><a href="/en/collections/shoes">Shoes</a></p>
    <p><a href="/en/collections/accessories">Accessories</a></p>

There are more logic functions available. [Click here to read more about logic functions.](http://support.storeflowhq.com/help/kb/templates/logic-functions)
There are more global variables available. [Click here to read more about global variables.](http://support.storeflowhq.com/help/kb/templates/global-variables)

### Content for Layout

Moving on to the next part:

    {% raw %}
    {{ content_for_layout }}
    {% endraw %}

With this tag you can tell the theme where to place the content from all the different templates, such as the product view, content page or search results. Simple and effective.

### Translations

And finally, we arrive at the last part:

    {% raw %}
    <p>Copyright {{ site.title }} - {{ 'all_rights_reserved' | translate }}.</p>
    {% endraw %}

Translations are a core element of Storeflow and you can translate any part of your theme. By using the translate helper you are telling Storeflow to look up the string 'all\_rights_reserved' in the language in which your customer is seeing your store. There are a number of predefined translations that you can use in your templates, but you can also create your own in the administration panel.

### Final Outcome

Here is the final outcome of our theme:

    {% raw %}
    <!DOCTYPE html>
    <html>
    <head>
      <title>My Store</title>
      <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
      <link href="http://static.storecdn.com/assets/0000/0001/theme/style.css" rel="stylesheet" type="text/css" media="all" />
    </head>
    <body>
      <h1>My Store</h1>

      <p><a href="/en/collections/womenswear">Womenswear</a></p>
      <p><a href="/en/collections/menswear">Menswear</a></p>
      <p><a href="/en/collections/shoes">Shoes</a></p>
      <p><a href="/en/collections/accessories">Accessories</a></p>

      Welcome to my store!

      <p>Copyright My Store - All Rights Reserved.</p>
    </body>
    </html>
    {% endraw %}

There are a lot more things you can do with the template engine so go ahead and read about all the different objects, helpers and variables in our template reference.

[Click here to access the template reference.](http://support.storeflowhq.com/help/kb/templates/template-reference)
