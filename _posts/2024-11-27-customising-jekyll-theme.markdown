---
layout: post
title:  "Getting started with Jekyll and customising minima"
date:   2024-12-08 18:00:00 +0000
categories: jekyll minima markdown html
---

This week I began using jekyll and was impressed by the ease with which I could set up a simple blog with the default `minima` theme and host it using github pages. If you are interested in setting up a blog like this one, see the [Jekyll quickstart][jekyll-docs]. 

For blogging alone, the default minima theme works perfectly but not all my projects can fit into a blog post. So I wanted to add a portfolio page. For this I used another section of the [Jekyll docs][jekyll-overriding] as a starting point and then looked at some other repositories that had a portfolio page. These included:

- Uri Shani's [website][uri-sh-site] and their [custom jekyll theme on GitHub][uri-sh-github]
- Tim Barry's [website][tim-barry-site] and [the associated GitHub repo][tim-barry-github]

I wanted to setup my website in such a way that I could just write markdown files in either the `_posts/` or `_portfolio/` folders and everything else would be taken care of automatically.

## Setting up the file structure

Following the advice in the [Jekyll docs][jekyll-overriding] I copied my layouts folder from the relevant folder on my computer (in my case: `/opt/homebrew/lib/ruby/gems/3.3.0/gems/minima-2.5.2` but check the [Jekyll docs][jekyll-overriding]) to find your version. Then I made a new [`portfolio.html`](https://github.com/frdrick/blog/blob/master/_layouts/portfolio.html) layout based on [`post.html`][post-layout-github].

## Changing the htmls

When changing these files I had to read up on the dot notation in html. But soon realised all my needs could be satisfied by specifying in yaml section at the top of my portfolio posts which elements of my portfolio I wanted displayed on the main page. For example, for my Landslide Project in the `yaml` I used:

```yaml
layout: page
title:  Landslide Susceptibility
tags: geospatial ArcGIS-Pro
summary: Using ArcGIS Pro to find the parts of Tamzoura most susceptible to landslides. 
image: ../assets/landslides/scenario3.jpg
width: 50%
caption: Relative level of susceptibility.
link: ../_portfolio/geospatial_data.markdown 
permalink: _portfolio/geospatial_data.markdown/ 
```

Some of these elements will change as I learn more about html and jekyll but currently:

- `summary` is the text shown on the main portfolio page.
- `tags` whilst currently unused I hope to allow for tag-based filtering of my portfolio when there are more of them
- `image` specifies a relative path to an image showing the kind of project in question
- `caption` is the caption below said image
- `link` and `permalink` together make the link to the post work. I plan on changing this soon becuase minima's [home.html][post-layout-github] file doesn't require this.

From here we can loop through the files in _portfolio and 

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
[jekyll-overriding]: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
[uri-sh-site]: https://urishx.github.io/
[uri-sh-github]: https://github.com/UriShX/Jekyll-portfolio
[tim-barry-site]: https://timothy-barry.github.io/
[tim-barry-github]: https://github.com/timothy-barry/timothy-barry.github.io
[post-layout-github]: https://github.com/frdrick/blog/blob/master/_layouts/home.html
