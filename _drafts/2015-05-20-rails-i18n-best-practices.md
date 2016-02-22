---
title: Rails I18n best practices
tags: [Ruby, Rails]
description: Get the most out of localizing your Rails app.
---

Rails gives us [localization features](http://guides.rubyonrails.org/i18n.html) via the rails-i18n gem. While the Rails guide describes the technical details on how to use it, it doesn't prescribe any guidelines on how to name and sort your localization strings. Here's my take on how a project's I18n strings should be sorted out.
{:.brief-intro.center}

* * * *

### Quote your strings
While the YAML format is liberal and quotation marks aren't needed, the consistency is always welcome. It also makes it less ambiguous for non-developers who may edit the YAML file.

```coffee
en:
  posts:
    index:
      title: "Blog posts"
      description: "These are the latest posts in the blog."
```

### Don't add punctuation
Some strings end in `:`. Don't place them in the YAML file. This will allow for the strings to be reusable later on.

```rb
t('.categories') + ":"
```

### Group by controller and action
Place your page's strings under their respective `controller` and `action` names. This allows to you take advantage of Rails's shortcuts. Also, always name your primary title as `title`.

```rb
# looks up 'posts.index.title', if you're on the posts#index view
t('.title')
```

### Group strings for partials
The same concept should apply for partials. You can also use the `t('.login')` shortcut inside partial views.

```coffee
en:
  shared:
    nav:
      back_to_home: "Back to home"
      login: "Log in"
```

### Avoid top-level strings
Don't place strings on the top level such as `t('and')`. Place them on a parent, even an arbitrary one. If you can't think of a parent name, use `common`.

```coffee
en:
  actions:
    submit: "Submit"
    add: "Add"
    delete: "Delete"
    login: "Log in"
  common:
    or: "or"
    and: "and"
```

### Avoid over nesting
Prefer to nest with just one level. Overly-complicated nesting can seem very arbitrary and confusing.

```coffee
# Avoid
en:
  user:
    mail:
      status:
        delivered: "Delivered"
        read: "Read"
```
  
```coffee
# Better
en:
  mail_status:
    delivered: "Delivered"
    read: "Read"
```
{:.light}

### Familiarize yourself with defaults
The default locale file is available under rails-i18n. [Read it](https://github.com/svenfuchs/rails-i18n/blob/master/rails/locale/en.yml).
  

<br>

## Time and date

### Don't use .strftime
Use i18n to format timestamps. Define your time formats in `time.formats`. Listed below are the default time formats available in Rails.

```rb
l(Time.now, format: :short)
```
{:.light}

```coffee
en:
  time:
    formats:
      default: "%a, %d %b %Y %H:%M:%S %z"
      short: "%d %b %H:%M"
```

### Same with dates
The `I18n.l` method also supports dates. Also, when creating new formats, add comments on what they should look like to help your teammates along.

```rb
l(Date.today, format: :long)
```
{:.light}

```yml
en:
  date:
    formats:
      default: "%Y-%m-%d" # 2015-06-25
      long: "%B %d, %Y"   # June 25, 2015
      short: "%b %d"      # Jun 25
```

<br>

## Forms

### Use ActiveRecord errors
The Rails method [full_messages](http://devdocs.io/rails/activemodel/errors#method-i-full_messages) looks up in predefined locations in your locale file. Take advantage of them. See [the cheatsheet](http://ricostacruz.com/cheatsheets/rails-i18n.html) for more.

```rb
person = Person.create
person.errors.full_messages
#=> ["Name is too short (minimum is 5 characters)",
#    "Name can't be blank", "Email can't be blank"]
```
{:.light}

```
activerecord.errors.models.[model_name].attributes.[attribute_name].[error]
activerecord.errors.models.[model_name].[error]
activerecord.errors.messages.[error]
errors.attributes.[attribute_name].[error]
errors.messages.[error]
```

### Use form labels
There are also conventions on where [f.label](http://devdocs.io/rails/actionview/helpers/formbuilder#method-i-label) will look up labels.

```rb
form_for @post do
  f.label :body
```
{:.light}

```coffee
helpers:
  # helpers.label.<model>.<field>
  label:
    post:
      body: "Your body text"
```
