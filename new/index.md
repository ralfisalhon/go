---
layout: page
title: Creating a New Link
description: "Instructions on how to install and customize the modern Jekyll theme HPSTR."
image:
  feature: abstract-11.jpg
modified: 2016-09-27
---

## Creating a New GO Link (V0.1)

We're working on automating this, but until then, there are a few steps to making a link.  Basically you make a pull request and add a file to our `_posts` folder.

___

### Setup

1. Check [/all](/all) to see if your link isn't taken (links are **not** case sensitive)
2. Setup a [Github](https://github.com/join) account if you don't have one.
3. Click here: [click](https://github.com/TuftsCSX/go.tufts.io/new/master/_posts)
4. If you see "You need to fork this repository", fork the repository (new github accounts will need to verify your email)

___

### Content

Copy the line below:

<script>
  var d = new Date();
  var year = d.getFullYear();
  var month = d.getMonth();
  if (month < 10) {
    month = "0" + month;
  };
  var day = d.getDay();
  if (day < 10) {
    day = "0" + day
  };
  document.write(year+"-"+month+"-"+day+"-[short link name].markdown");
</script>

Paste it here:

<img src="http://imgur.com/AzhCgSM.png" alt="">

Replace [short link name] with the shortened link name.  For example, in [go.tufts.io/csx](/csx), "csx" is the link name.  No spaces, capital letters don't matter, and only use numbers / letters / "-".

Copy this and replace the information in the square brackets:

```yaml
---
layout: links       # Don't touch this
permalink: /:title  # Don't touch this
title: [short link name (same as above)]
forward_to: http://[destination link here]
hidden: false       # Change to true if you don't want it to show on front page
author: [email]
---
[Optional description here]

```
Paste it here:

<img src="http://imgur.com/52PoM4f.png" alt="">

Double check that the name of the link is the same in the filename and the body:

<img src="http://imgur.com/smD666P.png" alt="">

__

### Making a Pull Request

1. Scroll to the bottom and hit "Propose New File"
2. Hit the big green "Create pull request" button
3. Add your name and tufts email in the box labeled "Leave a comment"
4. Hit the big green "Create pull request" button

And you're done! You'll have to wait a sec for us to approve the pull request, but feel free to ping me at richard@tufts.io

__

## Why Github?

* We don't want to maintain a server, so we're basically using Github for authentication
* You can edit a link with another pull request
* Most people have github accounts, so they won't have to create another account on another website
* Encourages people to make a github account and get some commits under their belt
* Interface with TuftsCSX github page
