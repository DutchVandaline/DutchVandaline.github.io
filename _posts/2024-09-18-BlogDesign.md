---
layout: single
title:  "Blog Design"
categories:
  - Others
---
<br>
I wanted to change the category of my tech blog but I didn't know how. I've looked up for modifying design on minimal mistakes through the keyword of 'minimal mistakes 사이드바'. The bottom url is the site which I've followed.
<br>
# Steps
## 1. /_data/navigation.yml
Modify the navigation.yml file. In my case, it looks like following. Top main is for upper bar. Ignore it.

```
# main links
main:
#   - title: "Quick-Start Guide"
#     url: https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/
#   - title: "About"
#     url: https://mmistakes.github.io/minimal-mistakes/about/
#   - title: "Sample Posts"
#     url: /year-archive/
#   - title: "Sample Collections"
#     url: /collection-archive/
#   - title: "Sitemap"
#     url: /sitemap/
sidebar-category:
  - title: "Category"
    children:
      - title: "Artificial Intelligence"
        url: "/AI"
      - title: "LeetCode"
        url:  "/LeetCode"
      - title: "App Development"
        url:  "/App"
      - title: "Other Projects"
        url:  "/Others"
```

## 2. Add categories for the _posts 
Modify the post's category. It took a long time and mucn errors on github because I have to modify all the files.

```
---
title:  "Blog Design"
categories:
  - Others
---
```

## 3. Add _pages directory
If there is no `_pages` directory, add one and make a file inside that directory named `category-{name}`. You need to modify every part of code which I've written 'Others' in the file.

```
---
title: "Others"
layout: archive
permalink: /Others
---


{% assign posts = site.categories.Others %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
```

## 4. Modify _config.yml

```
# Defaults
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: # true
      share: true
      related: true
      sidebar:                  # Added
        nav: "sidebar-category" # Added
```

https://x2info.github.io/minimal-mistakes/카테고리_만들기/
