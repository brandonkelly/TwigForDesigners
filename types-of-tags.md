# Types of Tags

All Twig tags follow a basic pattern that separates them from the surrounding HTML. At their outer edges you will find left and right curly braces, coupled with another character that signifies what _type_ of tag it is.

```jinja
{#     #}
{%     %}
{{     }}
```

There are three types of tags that Twig looks out for. In this chapter we’ll take a look at what those are and when you might use them.

## Comment Tags

You can use comment tags to leave little notes for yourself in the code. They are similar to HTML comments in that they won’t show up as rendered text in the browser, but unlike HTML comments they will never make it to the HTML source in the first place.

```jinja
<!-- This will be visible in the HTML source -->
{# This won’t! #}
```

## Logic Tags

Logic tags (often simply referred to as “tags”) define the _logic_ of your template, such as conditionals, loops, variable definitions, template includes, and other things.

Their syntax within the `{%` and `%}` varies from tag to tag, but they will always start with the same thing: the name of the tag. In their simplest form, that might be all that’s required. Take Craft’s {% requireLogin %} tag, for example:

```jinja
{# Gotta be logged in to visit this page #}
{% requireLogin %}
```

Other tags can accept parameters. In the case of Craft’s {% exit %} tag, you can optionally set the HTTP status code that should be sent to the browser in the response:

```jinja
{# This is not the page you are looking for #}
{% exit 404 %}
```

Some tags are meant to be used as a “tag pair”, which means that they expect to find a corresponding “closing tag” further down the template:

```jinja
{% autoescape %}
    Coffee is for closers.
{% endautoescape %}
```

Sometimes tags even support typing nested tags _between_ the opening and closing tags:

```jinja
{% if 212 > 42 %}
    Great job, Twig!
{% else %}
    Time to find a new templating system.
{% endif %}
```

## Output Tags

When you need to output something dynamically, use an output tag.

```jinja
{# Win ‘em over with kindness #}
You look nice today, {{ user.username }}
```

**Caution!** Remember that you never place an output tag (or any other tag for that matter) within another Twig tag:

```jinja
{# This won’t do what you think it will: #}
{{ "You look nice today, {{ user.username }}" }}

{# Either of these will do the trick, though: #}
{{ "You look nice today, " ~ user.username }}
{{ "You look nice today, #{user.username}" }}
```

We’ll go into further detail on how those work in [Strings].