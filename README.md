# ISL \<html\> Style Guide

Inspired by Nicolas Gallagher's [Idiomatic HTML](https://github.com/necolas/idiomatic-html).


## Table of contents

1. [General principles](#general-principles)
1. [Whitespace](#whitespace)
1. [Format](#format)
1. [Attribute order](#attribute-order)
1. [Naming](#naming)
1. [Django Templates](#django-templates)
1. [Practical example](#practical-example)
1. [License](#license)


## General principles

* All code in any code-base should look like a single person typed it, no
  matter how many people contributed.
* If in doubt when deciding upon a style, use existing, common patterns.


## Whitespace

* Use 4 spaces per indentation level, never tabs.
* Use blank lines as needed to make code more readable.
* Remove trailing whitespace.

Tip: configure your editor to "show invisibles" to eliminate end of line
whitespace and avoid polluting commits.


## Format

* Always use lowercase tag and attribute names.
* Write one discrete element per line.
* Use one additional level of indentation for each nested element.
* Use valueless boolean attributes (e.g. `checked` rather than
  `checked="checked"`).
* Always use double quotes to quote attribute values.
* Omit the `type` attributes from `link` stylesheet, `style` and `script`
  elements.
* Always include closing tags.
* Don't include a trailing slash in self-closing elements.

(Keep line-length to a sensible maximum, e.g., 80 columns.)

Example:

```html
<div class="tweet">
    <a href="path/to/somewhere">
        <img src="path/to/image.png" alt="">
    </a>
    <p>[tweet text]</p>
    <button disabled>Reply</button>
</div>
```


### Exceptions and slight deviations

Elements with multiple attributes can have attributes arranged across multiple
lines in an effort to improve readability and produce more useful diffs.

Example:

```html
<a class="[value]"
 data-action="[value]"
 data-id="[value]"
 href="[url]">
    <span>[text]</span>
</a>
```


## Attribute order

HTML attributes should be listed in an order that reflects the fact that class
names are the primary interface through which CSS and JavaScript select
elements.

1. `class`
2. `id`
3. `data-*`
4. Everything else

Example:

```html
<a class="[value]" id="[value]" data-name="[value]" href="[url]">[text]</a>
```


## Naming

Naming is hard, but very important. It's a crucial part of the process of
developing a maintainable code base, and ensuring that you have a relatively
scalable interface between your HTML and CSS/JS.

See <http://cssguidelin.es/#naming-conventions>.


## Django Templates

_Also applies to Jinja, Liquid, Swig, and Twig._

Put one (and only one) space between the curly brackets and the tag contents.

```twig
{{ foo }}
```

There should be no spaces between variables, pipes, and filters.

```twig
{{ foo|length }}
```

Control statements should be aligned with the HTML elements than they contain.
Removing the statement should result in HTML that is still aligned appropriately.

```twig
<ul>
    <li>John Doe<li>

    {% for user in users %}
    <li>{{ user.username }}</li>
    {% endfor %}
</ul>
```

The one exception being that content inside a __block__ should be indented one level.


## Practical example

An example of various conventions:

```twig
{# templates/index.html #}
{% extends 'layouts/default.html' %}

{% block content %}

    {% for post in posts if post.published %}

    <article class="post" id="post-{{ post.id }}">
        <time class="post__time timestamp">{{ post.pub_date }}</time>

        <a class="post__title"
         data-ga-category="{{ post.ga_category }}"
         data-id="{{ post.id }}"
         href="{{ post.url }}">{{ post.title }}</a>

        <div class="post__content">
            {{ post.excerpt }}
        </div>
    </article>

    {% endfor %}

{% endblock %}
```


## License

_ISL \<html\> Style Guide_ is licensed under the [Creative Commons Attribution
3.0 Unported License](http://creativecommons.org/licenses/by/3.0/). This applies
to all documents and translations in this repository.

Based on a work at <http://github.com/necolas/idiomatic-html>.
