---
layout: default
title: Template reference logic functions
description: Template reference logic functions
categories: templates
---


[&laquo; Back to reference index](http://support.storeflowhq.com/help/kb/templates/template-reference)

## Available logic functions

* if / else / unless
* case
* for loop

## Available template functions

* assign
* comment
* cycle
* include
* tablerow

## if / else / unless

You use the **if statement** when you need to check for something, for example if a product's price is greater than 0.

    {% raw %}
    {% if product.price > 0 %}
        This product will cost you {{ product.price | money_with_currency }}.
    {% else %}
        This product is free!
    {% endif %}
    {% endraw %}

You can also check for more than two possible outcomes by using **elsif**.

    {% raw %}
    {% if site.current_currency == 'USD' %}
        US Dollars
    {% elsif site.current_currency == 'EUR' %}
        Euros
    {% else %}
        Some other currency.
    {% endif %}
    {% endraw %}

## case

When you need to check for more than two possible outcomes, using the **if statement** can quickly become inconvenient to maintain. This is when you should consider the **case statement**.

    {% raw %}
    {% case site.current_currency %}
        {% when 'USD' %}
            US Dollars
        {% when 'EUR' %}
            Euros
        {% else %}
            Some other currency.
    {% endcase %}
    {% endraw %}

## for loop

When you need to go through a list of objects you use a **for loop**.

    {% raw %}
    {% for currency in site.currencies %}
      {{ currency.name }}
    {% endfor %}
    {% endraw %}

Results in:

    AUD
    EUR
    USD
    ZAR

You can restrict the number of items in your for loop by using the **limit** option:

    {% raw %}
    {% for currency in site.currencies limit:2 %}
      {{ currency.name }}
    {% endfor %}
    {% endraw %}

Results in:

    AUD
    EUR

You can also start the loop at a given offset using the **offset** option:

    {% raw %}
    {% for currency in site.currencies limit:2 offset:2 %}
      {{ currency.name }}
    {% endfor %}
    {% endraw %}

Results in:

    USD
    ZAR

When you are inside the loop you have access to the following variables:

* **forloop.length** &mdash; Number of items being looped through.
* **forloop.index** &mdash; Index of the current item in the loop. Counts from 1.
* **forloop.index0** &mdash; Index of the current item in the loop. Counts from 0.
* **forloop.rindex** &mdash; How many items are left? Counts from 1.
* **forloop.rindex0** &mdash; How many items are left? Counts from 0.
* **forloop.first** &mdash; Is this the first item?
* **forloop.last** &mdash; Is this the last item?

Example:

    {% raw %}
    {% for currency in site.currencies %}
      {{ forloop.index }} - {{ currency.name }} {% if forloop.first %}- first{% endif %}
    {% endfor %}
    {% endraw %}

Results in:

    0 - AUD - first
    1 - EUR
    2 - USD
    3 - ZAR

You can also loop through a certain range of numbers.

    {% raw %}
    {% for count in (1..4) %}
      {{ count }}
    {% endfor %}
    {% endraw %}

Results in:

    1
    2
    3
    4

## assign

Enables you to create your own variable.

    {% raw %}
    {% assign is_this_true = true %}
    {% if is_this_true == true %}
      This is true!
    {% endif %}
    {% endraw %}

Results in:

    This is true!

You can also create a variable from a block of HTML or template code, using the **capture** function.

    {% raw %}
    {% capture top_link %}<a href="#top">Go to top</a>{% endcapture %}

    {% for product in products %}
      <h1>{{ product.title }}</h1>
      {{ top_link }}
    {% endfor %}
    {% endraw %}

Results in:

    {% raw %}
    <h1>Storeflow T-shirt</h1>
    <a href="#top">Go to top</a>

    <h1>Storeflow Hoodie</h1>
    <a href="#top">Go to top</a>
    {% endraw %}

## comment

If you want to leave comments in your template, for yourself or anyone else editing the template, you can do so with the comment tag. Customers on your site will not see these comments.

    (c) Copyright MyStore {% comment %} Remember to add the year {% endcomment %}

## cycle

This is what you use when you want to highlight every other line in a list of items. You can also use cycling for any other purpose you see fit.

    {% raw %}
    {% for product in products %}
      <div class="product {% cycle 'normal', 'highlight' %}">
        {{ product.title }}
      </div>
    {% endfor %}
    {% endraw %}

Results in:

    {% raw %}
    <div class="product normal">
      Product No. 1
    </div>
    <div class="product highlight">
      Product No. 2
    </div>
    <div class="product normal">
      Product No. 3
    </div>
    {% endraw %}

You can also add an identifier for each cycle, allowing you to use multiple cycles.

    {% raw %}
    {% for product in products %}
      <div class="product {% cycle 'classname': 'normal', 'highlight' %}">
        {% cycle 'title': 'One', 'Two', 'Three' %}
      </div>
    {% endfor %}
    {% raw %}

Results in:

    {% raw %}
    <div class="product normal">
      One
    </div>
    <div class="product highlight">
      Two
    </div>
    <div class="product normal">
      Three
    </div>
    {% endraw %}

## include

Allows you to include a template file within another template file. In this example you would create a file called **product\_details.liquid** and save it in a folder called **snippets**. This is what the **product_details.liquid** file looks like:

    {% raw %}
    Title: {{ product.title }}
    Price: {{ product.price }}
    {{ note }}
    {% endraw %}

Then you can include that snippet in any other template file.

    {% raw %}
    {% for product in products %}
      {% include 'product_details' %}
    {% endfor %}
    {% endraw %}

This will automatically insert the contents of your **product_details.liquid** file into your current template. You can also change the value of the variables within the snippet.

    {% raw %}
    {% assign note = 'This is a note.' %}
    {% include 'product_details' %}
    {% endraw %}

## tablerow

Enables you to generate a row for an HTML &lt;table&gt;.

    {% raw %}
    <table>
      {{% tablerow collection in collections cols: 2 %}
        <td>
          {{ collection.title }}
        </td>
      {% endtablerow %}
    </table>
    {% endraw %}

Results in:

    {% raw %}
    <table>
      <tr>
        <td>
          Womenswear
        </td>
        <td>
          Menswear
        </td>
      </tr>
      <tr>
        <td>
          Shoes
        </td>
        <td>
          Accessories
        </td>
      </tr>
    </table>
    {% endraw %}
    
## Back to Index

[&laquo; Back to reference index](http://support.storeflowhq.com/help/kb/templates/template-reference)