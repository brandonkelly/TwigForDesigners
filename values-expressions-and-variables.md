# Values, Expressions, and Variabes

HTML supports several types of values. Most of them are textual (headings, paragraphs, etc.), but others are not (images and other media). You define what types of values you want to use by typing the appropriate HTML tag (`<h1>`, `<p>`, `<img>`).

Twig also has the concept of different value types. There are five in total:

- Strings
- Numbers
- Booleans
- Arrays
- Objects

Let’s take a look at each of those in detail.

### Strings

“String” is another word for “text”. To identify a string, you simply must wrap your text in either double or single quotes (but _not_ curly/smart quotes). Twig doesn’t care whether you go with double or single quotes, but if you start a string with double quotes, you also must end it with double quotes, and vise-versa.

Good strings:

    "Hello there."
    'Hello there.'

Bad strings:

    “Hello there.”
    "Hello there.'

Once you’ve started a string with a double quote, Twig will keep parsing it until it comes across another double quote. Which means that you can safely add any single quotes _inside_ the string, to be included in the actual value.

    "Brienne is like 7' tall!"
    'Give or take 5".'

If you need to use both types of quotes in the same string, you can place a backslash (`\`) right before the one that matches the string’s opening delimiter to “escape” it from being parsed as the closing delimiter.

    "Actually she’s exactly 6' 3\" tall."
    '6\' 3"? Must be some trick photography.'

### Numbers

Twig has support for a ton of numbers – 212, 7.5, and -10, just to name a few. Pretty much any number you can think of, though.

Unlike strings, numbers don’t have delimiters. You just type them out.

    212

### Booleans

“Booleans” (or “bools”) are either `true` or `false`. Those are reserved words in Twig, so if you want to create a boolean value, you just type it out.

    true
    false

### Arrays

Arrays are ordered lists of values. They are delimited with left and right square brackets (`[` and `]`), and their values are separated by commas.

    ['a', 'b', 'c', 'd', 'e']
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

 They can contain any types of values you want, including nested arrays and objects.

    [
        ['a', 'b', 'c'],
        ['d', 'e', 'f']
    ]

### Objects

Objects are similar to arrays, except that their values aren’t ordered numerically. Instead, you get to define the values’ indexes, or “keys”.

To define an object, use left and right curly braces as the delimiters (`{` and `}`). Separate your object’s key-value pairs with commas, like arrays, and separate the individual keys from the values with a colon.

    {
        name:        "Brienne",
        culture:     "Westerosi",
        birth_year:  "280AC",
        allegiances: ['House of Tarth', 'House Baratheon', 'House Stark', 'Rainbow Guard']
    }

We will go further into how to work with arrays and objects in [Arrays and Objects].

## Expressions

Remember mathematical expressions? You learned them back in second grade. The expression “2 + 2” is equal to 4. The expression “212 / 2” is equal to 106. And so on.

Expressions are a very powerful concept in Twig. They’re not just for doing math though – any time you need to combine multiple values together to create another value, you’re writing an expression.

For example, you can concatenate two strings together with a tilde (`~`):

    "Hello " ~ "there"

When Twig evaluates that, it will join the strings together into a single “Hello there” string before moving on.

Expressions can be nested as well. Remember PEMDAS? That same order of operations is built into Twig, so if you group an expression with parentheses, Twig will evaluate that sub-expression first, and then apply the resulting value to the outer expression.

Take this line for example:

    "I’m " ~ (2014-1985) ~ " years old."

The first thing Twig would do here is evaluate “2014-1985”, since it was in parentheses, and replace that sub-expression with the resulting value:

    "I’m " ~ 29 ~ " years old."

Next up it would join the two strings and number together to form one string:

    "I’m 29 years old."

And now we have our single resulting value!

## Variables

Variables are like _aliases_ for values. You get to pick their names, and you can assign them to whatever value (or expression) you want.

To define a variable, use the [`{% set %}`](http://twig.sensiolabs.org/doc/tags/set.html) tag.

```jinja
{% set title = "About Us" %}
```

The `{% set %}` tag syntax is made up of a custom variable name, followed by an equal sign, followed by the value/expression.

Once you’ve defined a variable, you can reference it at any point after that in your template, even within subsequent expressions.

```jinja
{% set title = "About Us" %}
{% set docTitle = title ~ " - ACME, Inc." %}

<html>
  <head>
    <title>{{ docTitle }}</title>
  </head>
  <body>
    <h1>{{ title }}</h1>
    <!-- ... -->
  </body>
</html>
```

The `{% set %}` tag also supports an alternative “tag pair” syntax, where the variable gets set to the resulting value between the `{% set %}` tag and a subsequent `{% endset %}` tag:

```jinga
{% set greeting %}
<p>Hello there.</p>
{% endset %}
```

That example would be roughly the same as typing:

```jinja
{% set greeting = "<p>Hello there.</p>" %}
```

The advantage of the tag pair is that you can place additional tags inside it:

```jinja
{% set greeting %}
  {% if gender == "m" %}
    <p>Hey there handsome!</p>
  {% else %}
    <p>Hey pretty lady!</p>
  {% endif %}
{% endset %}
```

We’ll be going into greater detail on ways to use variables in coming chapters.