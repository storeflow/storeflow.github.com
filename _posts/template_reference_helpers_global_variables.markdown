---
layout: default
title: Template reference helpers global variables
description: Template reference helpers global variables
categories: templates
---

[&laquo; Back to reference index](http://support.storeflowhq.com/help/kb/templates/template-reference)

Global objects and variables are accessible in any template at any time.

## Available global variables

* add\_to\_cart_url
* cart_url
* checkout_url
* collections &mdash; list of objects
* content\_for_layout
* currencies &mdash; list of objects
* current_page
* current_path
* current_url
* languages &mdash; list of objects
* meta_description
* meta_keywords
* meta_title
* pages &mdash; list of objects
* placeholders &mdash; list of objects
* query_string
* root_path
* search_url
* settings &mdash; list of objects
* site_url
* template

## add\_to\_cart_url

The URL used when adding a product to the cart.

`http://demo.mystoreflow.com/en/cart/add`

Can be used in a form:

<code>
    <form action="{{ add_to_cart_url }}" method="post">
      <input type="hidden" name="product" value="{{ product.id }}" />
      <input type="text" name="quantity" value="1" title="{{ 'quantity' | translate }}" />
      <input type="submit" value="{{ 'add_to_cart' | translate }}" />
    </form>
</code>

Can also be used in a link:

`<a link="{{ add_to_cart_url }}?product={{ product.id }}">{{ 'add_to_cart' | translate }}</a>`

However, using `link_to_cart` is a more proper way to create a link to add a product to the cart:

`{{ 'add_to_cart' | translate | link_to_cart: product }}`

## cart_url

The URL to the cart template.

`http://demo.mystoreflow.local/en/cart`

## checkout_url

The URL to the checkout page.

`http://demo.mystoreflow.local/en/cart/checkout`

## collections

All the collections in your store. Returns a list of `collection` objects.

## content_for_layout

By using this variable in a layout file, the template content 
XXX

## currencies

Every currency that Storeflow has to offer. Returns a list of `currency` objects.

## current_page

The current page in pagination.

## current_path

The path to the current page on the site, without the query string.

`/en/cart`

## current_url

The URL to the current page on the site, without the query string.

`http://demo.mystoreflow.com/en/cart`

## languages

Every language that Storeflow has to offer. Returns a list of `language` objects.

## meta_description

Meta description information from your site, product, collection and page settings.

## meta_keywords

Meta keywords information from your site, product, collection and page settings.

## meta_title

Meta title information from your site, product, collection and page settings.

## pages

All the pages in your store. Returns a list of `page` objects.

## placeholders

All the placeholders in your store. A placeholder is basically a menu with a list of pages. Returns a list of `placeholder` objects.

## query_string

The browser query string.

`search_query=t-shirt`

## root_path

The site's root path.

`/en`

## search_url

The URL to the search page.

`http://demo.mystoreflow.local/en/search`

Primarily used in a search form.

<code>
    <form action="{{ search_url }}" method="get">
      <input type="text" name="search_query" value="{{ search.query | escape }}" />
      <input type="submit" value="{{ 'search' | translate }}" />
    </form>
</code>

## settings

The JSON settings object for the template, which is generated from the settings.json file in the template's config directory.

`{{ settings.text_color }}`

Results in:

`#555555`

## site_url

The site's URL.

`http://demo.mystoreflow.local`

## template

The name of the current template file being rendered.

`product`

Available template names:

    404
    cart
    collection
    index
    page
    product
    search

## Back to Index

[&laquo; Back to reference index](http://support.storeflowhq.com/help/kb/templates/template-reference)