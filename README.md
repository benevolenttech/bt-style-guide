# ISL \<html\> Style Guide

*Principles of writing consistent, idiomatic HTML*


## Table of contents

1. [General principles](#general-principles)
1. [Whitespace](#whitespace)
1. [Format](#format)
1. [Attribute order](#attribute-order)
1. [Naming](#naming)
1. [Django/Jinja/Swig/Twig Templates](#djangojinjaswigtwig-templates)
1. [Practical example](#practical-example)
1. [License](#license)


## General principles

* All code in any code-base should look like a single person typed it, no
  matter how many people contributed.
* If in doubt when deciding upon a style, use existing, common patterns.

**[⬆ back to top](#table-of-contents)**


## Whitespace

* Use 4 spaces per indentation level.
* Remove trailing whitespace.

Tip: configure your editor to "show invisibles". This will allow you to
eliminate end of line whitespace, eliminate unintended blank line whitespace,
and avoid polluting commits.

**[⬆ back to top](#table-of-contents)**


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

**[⬆ back to top](#table-of-contents)**


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

**[⬆ back to top](#table-of-contents)**


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

**[⬆ back to top](#table-of-contents)**


## Naming

Naming is hard, but very important. It's a crucial part of the process of developing a maintainable code base, and ensuring that you have a relatively scalable interface between your HTML and CSS/JS.

See <http://cssguidelin.es/#naming-conventions>.


## Django/Jinja/Swig/Twig Templates

Put one (and only one) space between the curly brackets and the tag contents.

```
{{ foo }}
```

**[⬆ back to top](#table-of-contents)**


## Practical example

An example of various conventions.

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Document</title>
        <link rel="stylesheet" href="main.css">
        <script src="main.js"></script>
    </head>
    <body>
        <article class="post" id="1234">
            <time class="timestamp">March 15, 2012</time>
            <a data-id="1234"
             data-analytics-category="[value]"
             data-analytics-action="[value]"
             href="[url]">[text]</a>
            <ul>
                <li>
                    <a href="[url]">[text]</a>
                    <img src="[url]" alt="[text]">
                </li>
                <li>
                    <a href="[url]">[text]</a>
                </li>
            </ul>

            <a class="link-complex" href="[url]">
                <span class="link-complex__target">[text]</span>
                [text]
            </a>

            <input value="text" readonly>
        </article>
    </body>
</html>
```

**[⬆ back to top](#table-of-contents)**


## License

_Principles of writing consistent, idiomatic HTML_ by Nicolas Gallagher is
licensed under the [Creative Commons Attribution 3.0 Unported
License](http://creativecommons.org/licenses/by/3.0/). This applies to all
documents and translations in this repository.

Based on a work at
[github.com/necolas/idiomatic-html](https://github.com/necolas/idiomatic-html).

**[⬆ back to top](#table-of-contents)**

