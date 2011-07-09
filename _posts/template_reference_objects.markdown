---
layout: default
title: Template reference objects
description: Template reference objects
categories: templates
---

[&laquo; Back to reference index](http://support.storeflowhq.com/help/kb/templates/template-reference)

## Available objects

* cart
* cart_item
* collection
* currency
* current_currency
* current_language
* language
* page
* placeholder
* product
* search
* site
* variant
* variant_option
* variant_type
* vendor

## cart

The customer's shopping cart. When a customer adds a product to their cart the product becomes an item.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
cart.id                               | Unique integer ID.
cart.is_empty                         | Is true if there are no items in the cart.
cart.items                            | All the items in the cart. Returns a list of `cart_item` objects. Can be looped through.
cart.number\_of_items                 | Number of all the items in the cart.
cart.sub_total                        | Total amount of the cart, without discounts.
cart.total\_discount_amount           | Discount amount of the cart.
cart.total_price                      | Total amount of the cart, including discounts.

## cart_item

An item in a customer's shopping cart. An item is basically a representation of a product in your store.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
cart_item.id                          | Unique integer ID.
cart_item.price                       | Price of the item at the time it was added to the cart.
cart_item.product                     | Product which the item represents.
cart_item.quantity                    | Quantity of the item.
cart_item.sku                         | Product SKU (or the variant SKU if the product has variants).
cart_item.title                       | Product title (or the variant title if the product has variants).
cart_item.total\_price                | Total item amount, including discounts.
cart_item.variant                     | Product variant.
cart_item.variant\_title              | Product variant title.


## collection

Collection in your store. You can get all collections for your store `{% for collection in collections %}` or you can look up a specific collection by its handle `{% for product in collections.frontpage.products %}`.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
collection.id                         | Unique integer ID.
collection.handle                     | Collection handle, used when looking for a specific collection, e.g. `{{ collections.t-shirts }}`.
collection.description                | Collection description.
collection.meta_description           | Meta description.
collection.meta_keywords              | Meta keywords.
collection.meta_title                 | Meta title.
collection.path                       | Path to the collection, e.g. /en/t-shirts.
collection.products                   | All the products in the collection. Returns a list of `product` objects. Can be looped through.
collection.title                      | Collection title.
collection.url                        | Full URL to the collection, e.g. http://demo.mystoreflow.com/en/t-shirts.

## currency

Specific currency.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
currency.code                         | ISO code of the currency, e.g. USD, EUR.
currency.name                         | Currency name, e.g. United States Dollar.
currency.url                          | URL when a customer switches to this currency.

## current_currency

Represents the currently selected currency for your store. If the customer hasn't selected a currency, your store's default currency is used. Returns a currency object and therefore has the same properties.

## current_language

Represents the currently selected language for your store. If the customer hasn't selected a language, your store's default language is used. Returns a language object and therefore has the same properties.

## language

Specific language.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
language.code                         | ISO code of the language, e.g. en, es.
language.flag                         | Flag image name of the language, e.g. en.png, es.png. Can be used with the `flag_img_url` helper.
language.name                         | Language name, e.g. English.
language.url                          | URL when a customer switches to this language.

## page

Content page in your store.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
page.id                               | Unique integer ID.
page.content                          | Page content.
page.handle                           | Page handle, used when looking for a specific page, e.g. `{{ pages.about-us }}`.
page.is_open                          | Is true if the page is being viewed in the browser.
page.meta_description                 | Meta description.
page.meta_keywords                    | Meta keywords.
page.meta_title                       | Meta title.
page.path                             | Path to the page, e.g. /en/pages/about-us.
page.title                            | Page title.
page.url                              | Full URL to the page, e.g. http://demo.mystoreflow.com/en/pages/about-us.

## placeholder

A placeholder is basically a menu with a list of pages. There are two types of placeholders, one for the main menu and one for the footer. By looking up a placeholder by its handle you can get the list of pages `{% for page in placeholders.main_menu.pages %}`.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
placeholder.id                        | Unique integer ID.
placeholder.handle                    | Placeholder handle ('main_menu', 'footer').
placeholder.pages                     | All the pages in the placeholder. Returns a list of `page` objects. Can be looped through.

## product

A product in your store.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
product.id                            | Unique integer ID.
product.is_available                  | Is true unless the product is sold out.
product.collections                   | All the collections you have included this product in. Returns a list of `collection` objects. Can be looped through.
product.is\_coming_soon               | Is true if the product was marked 'coming soon'.
product.coming\_soon\_expected_date   | Expected date of arrival, if set.
product.current\_stock_level          | Number of items left in stock.
product.description                   | Product description.
product.discount                      | Discount amount. If the product has variants you can get the discount amount for each variant.
product.featured\_image               | Featured image. Can be used with the `product_img_url` helper, e.g. `{{ product.featured_image | product_img_url: 'xlarge' }}`.
product.handle                        | Product handle, used when looking for a specific product, e.g. `{{ products.storeflow-t-shirt }}`.
product.has_discount                  | Is true if the product has a discounted price.
product.has_variants                  | Is true if the product has variants.
product.images                        | All the images for the product. Can be looped through and used with the `product_img_url` helper.
product.is\_low\_in_stock             | Is true if there are only a few items left in stock.
product.meta_description              | Meta description.
product.meta_keywords                 | Meta keywords.
product.meta_title                    | Meta title.
product.path                          | Path to the product, e.g. /en/products/storeflow-t-shirt.
product.price                         | Product price. If the product has variants this is the lowest price.
product.price_min                     | Lowest price of all of the product variants.
product.price_max                     | Highest price of all of the product variants.
product.regular_price                 | If there is any discount, regular price is the original product price.
product.title                         | Product title.
product.url                           | Full URL to the product, e.g. http://demo.mystoreflow.com/en/products/storeflow-t-shirt.
product.variant_types                 | All the variant types for the variant of the product, e.g. Color, Size. Can be looped through.
product.variants                      | All the variants of the product. Returns a list of `variant` objects. Can be looped through.
product.vendor                        | Product vendor. Returns a `vendor` object.

## search

This object represents search results.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
search.was_performed                  | Is true if a search was performed.
search.products                       | All the products found. Returns a list of `product` objects. Can be looped through.
search.query                          | The search query typed in by the customer.
search.terms                          | Array of all the terms in the search query.

## site

Your store information and settings.

Property                                      | Description
--------------------------------------------- | ---------------------------------------------------------------
site.available_currencies                     | Available currencies for the store.
site.available_languages                      | Available languages for the store.
site.domain                                   | Store domain with the http:// part, e.g. demo.mystoreflow.com or www.yourdomain.com.
site.has\_many_currencies                     | Is true if the store has more than one currency available.
site.has\_many_languages                      | Is true if the store has more than one language available.
site.languages                                | Available languages for the store.
site.meta_description                         | Meta description.
site.meta_keywords                            | Meta keywords.
site.meta_title                               | Meta title.
site.has\_taxes\_included\_in\_product_prices | Is true is taxes are included in all of the store's product prices.
site.title                                    | Site title.
site.url                                      | Full URL to the site, e.g. http://demo.mystoreflow.com or http://www.yourdomain.com.

## variant

Variant of a specific product, such as a Black T-shirt in Small.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
variant.id                            | Unique integer ID.
variant.is_available                  | Is true unless the variant is sold out.
variant.current\_stock_level          | Number of items left in stock in this variant.
variant.discount                      | Variant discount amount.
variant.is\_low\_in_stock             | Is true if there are only a few items left in stock in this variant.
variant.options                       | All the variant options for this variant, e.g. "Black, Small", "Black, Medium". Returns a list of `variant_option` objects. Can be looped through.
variant.price                         | Variant price.
product.regular_price                 | If there is any discount, regular price is the original variant price.
variant.sku                           | Variant SKU.
variant.title                         | Variant title, e.g. "Black, Small", "Black, Medium"
variant.weight                        | Variant weight.

## variant_option

An option for a variant, such as Black, White, Blue for the variant type Color.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
variant_option.id                     | Unique integer ID.
variant_option.title                  | Variant option title, e.g. Black, White.

## variant_type

Variant type, such as Color, Size.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
variant_type.id                       | Unique integer ID.
variant_type.options                  | All the variant options for this variant type. Returns a list of `variant_type` objects. Can be looped through.
variant_type.title                    | Variant type title, e.g. Color, Size.

## vendor

Vendor in your store.

Property                              | Description
------------------------------------- | ---------------------------------------------------------------
vendor.id                             | Unique integer ID.
vendor.description                    | Vendor description.
vendor.handle                         | Vendor handle, used when looking for a specific vendor, e.g. `{{ vendors.storeflow }}`.
vendor.products                       | All the products belonging to this vendor. Returns a list of `product` objects. Can be looped through.
vendor.title                          | Vendor title.
vendor.url                            | Full URL to the vendor, e.g. http://demo.mystoreflow.com/en/vendors/storeflow.

## Back to Index

[&laquo; Back to reference index](http://support.storeflowhq.com/help/kb/templates/template-reference)