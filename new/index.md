---
layout: page
title: Creating a New Link
description: "Instructions on how to install and customize the modern Jekyll theme HPSTR."
image:
  feature: abstract-11.jpg
modified: 2016-06-01T15:14:43-04:00
---

TODO: make this about how to create a new thing

## Basic Setup for a new Jekyll site

1. [Install Bundler](http://bundler.io) `gem install bundler` and then install [Jekyll](http://jekyllrb.com) and all dependencies `bundle install`.

<div markdown="0"><a href="https://github.com/mmistakes/hpstr-jekyll-theme/archive/master.zip" class="btn">Download the Theme</a></div>

**Pro-tip:** tip
{: .notice}

---

## Running Jekyll

```bash
code
```


## Customization

Most of the variables found here are used in the .html files found in `_includes` if you need to add or remove anything. A good place to start would be to add the `title`, `description`, and `url` for your site. Links are absolute and prefixed with `{{ "{{ site.url " }}}}` in the various `_includes` and `_layouts`, so remember to properly set `url`[^1] to `http://localhost:4000` when developing locally.

```yaml
comments: false
```
---

## Questions?

Having a problem getting something to work or want to know why I setup something in a certain way? Ping me on Twitter [@mmistakes](http://twitter.com/mmistakes) or [file a GitHub Issue](https://github.com/mmistakes/hpstr-jekyll-theme/issues/new). And if you make something cool with this theme feel free to let me know.

---

## License

This theme is free and open source software, distributed under the [MIT License]({{ site.url }}/LICENSE) version 2 or later. So feel free to to modify this theme to suit your needs.

---

[^1]: Used to generate absolute URLs in `feed.xml`, and for canonical URLs in `head.html`. Don't include a trailing `/` in your base url ie: http://mademistakes.com. When developing locally I suggest using http://localhost:4000 or whatever localhost you're using to properly load all theme stylesheets, scripts, and image assets. If you leave this variable blank all links will resolve correctly except those pointing to home.

[^2]: If you're using GitHub Pages to host your site be aware that plugins are disabled. So you'll need to build your site locally and then manually deploy if you want to use this sweet plugin.
