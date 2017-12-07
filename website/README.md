---
currentMenu: home
---

# Couscous template for Uniter

This template is used for the Uniter library documentation. It is based off of the [standard Couscous 'Native' template](https://github.com/pnowy/CouscousNativeTemplate).

![](screenshot.png)

## Usage

To use the template, set it up in your `couscous.yml` configuration file:

```yaml
template:
    url: https://github.com/pnowy/CouscousNativeTemplate
```

## Configuration

Here are all the variables you can set in your `couscous.yml`:

```yaml
# Base URL of the published website
baseUrl: http://username.github.io/project

# Used to link to the GitHub project
github:
    user: myself
    repo: my-project

title: My project
subTitle: This is a great project.
# the icon next to page title from Font Awesome library
fontAwesomeIcon: fa fa-hand-peace-o
footerText: This is a footer text
googleAnalyticsCode: GOOGLE-ANALYTICS-CODE

# The left menu bar
menu:
    sections:
        main:
            name: Main documentation
            items:
                home:
                    text: Home page
                    # You can use relative urls
                    relativeUrl: doc/faq.html
                foo:
                    text: Another link
                    # Or absolute urls
                    absoluteUrl: https://example.com
        other:
            name: Other topics
            items:
```

Note that the menu items can also contain HTML:

```yaml
home:
    text: "<i class='fa fa-github'></i> Home page"
    relativeUrl: doc/faq.html
```

## Menu

To set the current menu item (i.e. highlighted menu item), set the ```currentMenu```
key in the Markdown files:

```
markdown
---
currentMenu: home
---

# Welcome
```
