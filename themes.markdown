---
layout: doc
title: Themes Documentation
---





# <span>Themes</span> Documentation

This documentation is for creating custom themes in PortfolioDeck. Don't hesitate to drop us a line if you got any questions or comments. Send an email to <hello@portfoliodeck.com>.

We use [Liquid](http://www.liquidmarkup.org/) as our templating language. If you ever have designed themes in [Shopify](http://www.shopify.com/?ref=winston) you've used it. If you're new to Liquid, please take a couple of minutes to read through [Liquid for designers](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers). Don't worry, we'll wait. Done? Good, let's proceed.




## Contents

* [Templates and assets](#templates)
* [Global objects](#global)
* [Template specific objects](#template_objects)
* [Filters](#filters)
* [Image sizes](#sizes)





## Templates and assets ## {#templates}

A theme consists of six template files and accompanying assets (stylesheets, javascripts and graphics). There is a template for each page type. There is also a layout template for the framework of the site (header, navigation and footer). Each page template is rendered inside the layout template.

* [layout.liquid](#layout_template)
* [index.liquid](#index_template)
* [collection.liquid](#collection_template)
* [set.liquid](#set_template)
* [item.liquid](#item_template)
* [page.liquid](#page_template)

### layout.liquid ### {#layout_template}

The layout template is used to set the framework for the site. This is were you'll place all the elements that should be available on every page of your site. E.g. logo, navigation, footer. It is also in this template that you write your `<html>`, `<head>` and `<body>` tags.

#### Available objects

* [Global objects](#global)

### index.liquid ### {#index_template}

The index template is your sites front-page.

#### Available objects

* [Global objects](#global)

### collection.liquid ### {#collection_template}

This template renders a collections page. The main purpose of this page would most likely be to show the sets in a collection.

#### Available objects

* [Global objects](#global)
* [Collection](#collection_object)

### set.liquid ### {#set_template}

This template renders a set page. On this page you can, for example, show the first item in the set or an overview of all items in the set.

#### Available objects

* [Global objects](#global)
* [Set](#set_object)

### item.liquid ### {#item_template}

This template renders an item page. An item is an image that you have uploaded and placed in a set. On this page you might want to render the image in your preferred size and display title and description.

#### Available objects

* [Global objects](#global)
* [Item](#item_object)

### page.liquid ### {#page_template}

The template renders one of your static pages.

#### Available objects

* [Global objects](#global)
* [Page](#page_object)







## Global objects ## {#global}

These objects are available in all template files.

* `portfolio`
* `contact`
* `collections`
* `sets`
* `page_title`

### Portfolio

* `portfolio.name` <br>Returns a string with the name you choose for your portfolio. To change your portfolio name go to Customize and click ”Edit info”.
* `portfolio.description` <br>Returns a string with your description/tagline. The description can be changed in the same location as the name.
* `portfolio.url` <br>Returns the full url to your portfolio.

### Contact

The `contact` object contains all your contact details supplied under Customize / Your Info.

* `contact.email`
* `contact.phone`
* `contact.url` <br>Returns the web address supplied under contact details. This is __not__ the same as `portfolio.url`.
* `contact.address`
* `contact.post_code`
* `contact.city`
* `contact.country`
* `contact.twitter` <br>Returns an url to your twitter (if supplied).
* `contact.facebook` <br>Returns an url to your Facebook profile (if supplied).

### Collections

The `collections` object is available in all templates. It contains a list of all collections in the portfolio. You can also retrieve a specific collection with its `handle` e.g. `collections.main`, where `main` is the handle, will return the `collection` with the handle `main`. [Check out the docs for the collection object](#collection_object). 

For example, if you want to create a list of links to all your collections:

<div style="display: none;">
For some stupid reason this is necessary so that Jekyll do not parse the following examples as liquid.
{{ '{% if collections != empty %}' }}
</div>

    {% if collections != empty %}
      <ul>
      {% for _collection in collections %}
        <li><a href="{{ _collection | path }}">{{ _collection.title }}</a></li>
      {% endfor %}
      </ul>
    {% endif %}

### Sets

The `sets` object is available in all templates. It contains a list of all sets in the portfolio. You can also retrieve a specific `set` with its `handle` (e.g. `sets.main`, where `main` is the handle). [Check out the docs for the set object](#set_object). 

For example, if you wanted to create a list of links to all your sets:

    {% if sets != empty %}
      <ul>
      {% for _set in sets %}
        <li><a href="{{ _set | path }}">{{ _set.title }}</a></li>
      {% endfor %}
      </ul>
    {% endif %}

### Pages

The `pages` object is available in all templates. It contains a list of all pages in the portfolio. You can also retrieve a specific `page` with its `handle` (e.g. `pages.main`, where `main` is the handle). [Check out the docs for the page object](#page_object). 

For example, if you wanted to create a list of links to all your pages:

    {% if pages != empty %}
      <ul>
      {% for _page in pages %}
        <li><a href="{{ _page | path }}">{{ _page.title }}</a></li>
      {% endfor %}
      </ul>
    {% endif %}

### Page_title

`page_title` returns a string with the title of the current page. If the current page is a `set` it returns the `set.title` and so on for `page`, `collection` and `item`.




## Template specific objects ## {#template_objects}

* `collection`
* `set`
* `item`
* `page`

### Collection ### {#collection_object}

The current collection is retrieved with `collection`. It is available in the `collection.liquid` template. These variables are available on the collection object:

* `collection.title` <br>Returns a string with the collections title.
* `collection.description` <br>Returns a string with the collections description.
* `collection.uri` <br>Returns a string with the <span class="caps">URI</span> for the collection.
* `collection.sets` <br>Returns an array with the sets in the collecti[.

### Set ### {#collection_set}

The current set is retrieved with `set`. It is available in the `set.liquid` template. These are the available variables on the set object:

* `set.title` <br>Returns a string with the sets title.
* `set.description` <br>Returns a string with the sets description.
* `set.cover` <br>Returns a object with the sets cover image.
* `set.items` <br>Returns an array with the items in the set.

### Item ### {#item_object}

The current item is retrieved with `item`. It is available in the `item.liquid` template. These variables are available on the item object:

* `item.title` <br>Returns a string with the items title.
* `item.description` <br>Returns a string with the items description.
* `item.width` <br>Returns an integer with the width of the original.
* `item.height` <br>Returns an integer with the height of the original.
* `item.landscape` <br>Returns <span class="caps">TRUE</span> if width > height.
* `item.portrait` <br>Returns <span class="caps">TRUE</span> if width < height.
* `item.next_item` <br>Returns an object with the next item in the set.
* `item.previous_item` <br>Returns an object with the previous item in the set.
* `item.set` <br>Returns an object with the set the item belongs.
* `item.position`<br>Returns an integer with the `items` position in relation to the other items in the set[

### Page ### {#page_object}

The current page is retrieved with `page`. It is available in the `page.liquid`. These are the available objects:

* `page.title` <br>Returns a string with the page title.
* `page.body` <br>Returns a string with the pages body content.




## Filters ## {#filters}

This is the filters we have set up specifically for PortfolioDeck. Liquid also has its own [standard filters](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers).

* `path`
* `path_with_collection`
* `asset_tag`

### Path

The `path` filter is used to get the address for a `collection`, `set`, `item` or `page`. Example:

    <a href="{{ collection | path }}">{{ collection.title }}</a>
    Output:
    <a href="/collection/the-title">The Title</a>

### Path_with_collection

The ` path_with_collection ` filter is used to get the address for a `set` or `item` with the parent `collection` added to the address. Example:

    <a href="{{ set | path_with_collection: collection }}">{{ set.title }}</a>
    Output:
    <a href="/collection/collection-title/set/set-title">The Title</a>

### Asset_tag

The `asset_tag` filter is used to get the <span class="caps">HTML</span> for an item. Example:

    {{ item | asset_tag: `685` }}
    Output:
    <img src="http://images.portfoliodeck.com/assets/685/RESIZE_TOKEN/1.jpg" alt="Item Title" width="685" height="400">


### Image_url

The `image_url` filter is used get the url for a item. Example

	{{ item | image_url: `w400` }}
	Output:
	http://images.portfoliodeck.com/assets/w400/RESIZE_TOKEN/1.jpg

	{{ set.cover | image_url: `80` }}
	Output:
	http://images.portfoliodeck.com/assets/80/RESIZE_TOKEN/2.jpg



## Image sizes ## {#sizes}

As you see in the example above we supply `685` to the asset tag. This is the size the asset will be displayed in. There are a couple of different ways to get the desired size.

* `685` <br>Renders the image within a 685px square. If the image is in landscape format it will be 685px wide. An image in portrait format will be 685px high.
* `685x500` <br>Renders the image within a rectangle with a width of 685px and a height of 500px.
* `w685` <br>Renders the image with a width of 685px.
* `h685` <br>Renders the image with a height of 685px.
* `c200x250` <br>Renders the image cropped to 200px width and 250px height.

### Examples

    {{ item | asset_tag: `w685` }}

	{{ item | image_url: `w400` }}
