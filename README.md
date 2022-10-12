
# This is the codebase for NHS CYPMHS prototype V5

## Extra nunjucks code

I have added a couple of extra includes to the codebase in order to take some of the tedium out of replicating the sub navigations on every page.

These are in apps/views/includes and are named:
- sub-topic-nav.html
- mini-step-nav.html

I have set these up to basically run through a loop and add or omit classes IF a the current page name is equal to the nav item page name. This adds the current code, i.e.

`{% if page_title == item.title %}`

### What needs to be done to make this work

In order for these to work there needs to an extra couple of lines of code at the top of in each page declaring it's name and parent page using the set tag:

`{% set parent_page_title = "Mental health support for children and young people" %}`<br>
`{% set page_title = "Steps for getting help" %}`

An array is set up in the include navigation file which declare the aforementioned page titles, ids, urls

`{% set arr = [` <br>
  `{ title: "Children and young people's (CYP) mental health services", id: 1,  url: "/cypmh-services" },` <br>
  `{ title: "Steps for getting help", id: 2,  url: "/steps-for-getting-help" },` <br>
  `{ title: "Charity and other services", id: 3,  url: "/charities-and-other-services" },` <br>
  `{ title: "Information for parents and carers", id: 4,  url: "/support-for-parents" }` <br>
  `] %}`

**N.B.** THIS WORKS AS LONG AS, THE **item.title**  NAME IN THE INCLUDE AND THE **set page_title** NAME AT THE TOP OF THE RELEVANT PAGE, HAVE THE EXACT SAME VALUES.

This is then looped thorough the array with some **If/Else** logic to make sure that the current page class is applied to the current page else ignore and if it is the current page then don't apply underlines.

`<aside class="nhsuk-grid-column">`<br>
  `<div id="sibling-nav" class="app-related-nav beta-hub-sibling-nav nhsuk-u-padding-top-5">`<br>
    `<h2 class="app-related-nav__heading nhsuk-u-padding-bottom-3">More in <a href="">{{ topic_title }}</a></h2>`<br>
    `<nav role="navigation" class="app-related-nav__nav-section">`<br>
    `<ul class="app-related-nav__list beta-hub-sibling-nav__list">`<br>
      `{% for item in arr %}`<br>
     ` <li class="beta-hub-sibling-nav__item {% if page_title == item.title %} beta-hub-sibling-nav--current {% endif %}">{% if page_title == item.title %}{% else %}<a href="{{ item.url }}">{% endif %}{{ item.title }}{% if page_title == item.title %}{% else %}</a>{% endif %}</li>`<br>
      `{% else %}`<br>
     ` <li class="beta-hub-sibling-nav__item">Nothing to see here</li><br>
      {% endfor %}`<br>
    `</ul>`<br>
  `</nav>`<br>
`</div>`<br>
`</aside>`<br>

in the navigation bottom of the relevant child pages this is added

`{% include "includes/sub-topic-nav.html" %}`

#### Mini steps navigation

The same has been done for the min-steps include (**includes>mini-step-nav.html**) with the addition of a position in the initial array

`{% set arr = [` <br>
  `{title: "Seeking help - what you need to do", id: 1,  url: "/seeking-help", position: 1 },` <br>
  `{ title: "Having a conversation with a mental health professional", id: 2,  url: "/having-a-conversation", position: 2 },` <br>
  `{ title: "Getting advice and help for your needs", id: 3,  url: "/getting-advice", position: 3 },` <br>
  `{ title: "Waiting for help", id: 4,  url: "/waiting-for-help", position: 4 },` <br>
  `{ title: "Moving on", id: 5,  url: "/moving-on", position: 5 }` <br>
  `] %}` <br>

## Also

There are copies of V1-4 of the prototype in apps > views with the rest of v5 code


<!-- Visit the <a href="http://nhsuk-prototype-kit.azurewebsites.net/docs">NHS.UK prototype kit site</a> to download the latest version and read the documentation.

## Security

 If you publish your prototypes online, they must be protected by a <a href="http://nhsuk-prototype-kit.azurewebsites.net/docs/how-tos/heroku">username and password</a>. This is to prevent members of the public finding prototypes and thinking they are real services.

You must protect user privacy at all times, even when using prototypes. Prototypes made with the kit look like NHS.UK, but do not have the same security provisions. Always make sure you are handling user data appropriately.

## Installation instructions

- <a href="http://nhsuk-prototype-kit.azurewebsites.net/docs/install/simple">Install guide (non technical)</a>
- <a href="http://nhsuk-prototype-kit.azurewebsites.net/docs/install/advanced">Developer friendly install guide (technical)</a>

## Contribute

If you want to contribute to the NHS.UK prototype kit, by reporting bugs, fixing bugs, suggesting new features or writing documentation, then read our [contributing guidelines](CONTRIBUTING.md).

## Development enviroment

[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/nhsuk/nhsuk-prototype-kit)

-->
