## What you need

- [Liquid Templating Engine](https://shopify.github.io/liquid/)
- [Liquid-Rails](https://github.com/mikoweb/liquid4-rails)
- [Liquid Blocks](https://github.com/mikoweb/liquid4-blocks)
- [Liquid extensions](https://github.com/mikoweb/liquid-rails-extensions)
- [Liquid for Programmers](https://github.com/shopify/liquid/wiki/liquid-for-programmers)

## Gemfile

Add to file:

    gem 'liquid', '>= 4.0.0.rc2'
    gem 'liquid4-blocks', '~> 0.7.0'
    gem 'liquid-rails-extensions', '~> 0.0.4'

## Template handler

Create the following file `config/initializers/liquid_template_handler.rb`:

    require 'liquid'
    require 'liquid_blocks'
    require 'liquid4-rails'
    require 'liquid-rails-extensions'

## How to use

Create base template `app/views/layouts/_base.liquid`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>{% block title %}Default title{% endblock %}</title>
    {% block stylesheets %}{{ 'application'|stylesheet_link_tag }}{% endblock %}
    {% csrf_meta_tags %}
</head>
<body>
{% block body %}{% block content %}{% endblock %}{% endblock %}
{% block javascripts %}{{ 'application'|javascript_include_tag }}{% endblock %}
</body>
</html>
```

Your view template `app/views/sample/index.liquid`:

```html
{% extends "layouts/base" %}

{% block content %}
    <a href="{{ 'root'|path }}">{{ 'hello'|translate }}</a>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
{% endblock %}

{% block javascripts %}
    {{ block.super }}
    <script type="text/javascript">console.log('Hello, World!');</script>
{% endblock %}
```
