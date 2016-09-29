---
layout: page
title: Creating a New Link
description: "Instructions on how to install and customize the modern Jekyll theme HPSTR."
image:
  feature: abstract-11.jpg
modified: 2016-09-27
---

<head>
  {% include link-checker.html %}
  {% include global-scripts.html %}
  <script type="text/javascript">
    window.onload = function() {
      var params = ['url', 'shorturl', 'email', 'description'];

      for (i = 0; i < params.length; i++) {
        var p = getParameterByName(params[i]);
        if (p) {
          document.getElementById(params[i] + "-input").value = p;
          changeContentText();
        }
      }
    }
  </script>
</head>

## Creating a New GO Link (V0.1)

We're working on automating this, but until then, there are a few steps to making a link.  Basically you make a pull request and add a file to our `_posts` folder.

___

### Setup

1. Check [/all](/all) to see if your link isn't taken (links are **not** case sensitive)
2. Setup a [Github](https://github.com/join) account if you don't have one.
3. Open the [file creation page](https://github.com/TuftsCSX/go.tufts.io/new/master/_posts)
4. If you see "You need to fork this repository", fork the repository (new github accounts will need to verify your email)

___

### Content

Fill the form below and we'll generate the appropriate text for you to copy / past:

<script type="text/javascript">
  var today = new Date();

  function changeContentText() {
    var url = document.getElementById('url-input').value;
    var shorturl = document.getElementById('shorturl-input').value;
    var email = document.getElementById('email-input').value;
    var desc = document.getElementById('description-input').value;
    var hidden = document.getElementById('is-hidden-checkbox').checked;

    var year = today.getFullYear();
    var month = today.getMonth()+1;
    var day = today.getDate();
    if (month < 10) {
      month = "0" + month;
    };
    if (day < 10) {
      day = "0" + day
    };

    if (url.indexOf("://") == -1) {
      url = "http://"+url
    }

    var fileName = year+"-"+month+"-"+day+"-"+shorturl+".markdown";
    var bodyText = "---\nlayout: links\npermalink: /:title\nforward_to: " + url +"\nhidden: "+hidden+"\nauthor: " + email +"\n---\n"+desc;

    document.getElementById('content-title-text').innerHTML = fileName;
    document.getElementById('content-body-text').innerHTML = bodyText;
    showErrorMessages(url, shorturl, email);
  }

  function emailErrors(email) {
    if (email.length == 0) {
      return "Tufts email required";
    } else if (email.indexOf("@tufts.edu") == -1) {
      return "Must include at least 1 Tufts email";
    } else {
      return "None";
    }
  }

  function showErrorMessages(url, shorturl, email) {
    var result = "Errors:<ul style='margin-top:0px'>";
    var div = document.getElementById('form-errors');
    var errorCount = 0;

    if (url.length <= 7) {
      errorCount += 1;
      result += "<li>Url required</li>";
    }

    var shortError = shorturlErrors(shorturl);
    if (shortError != "None") {
      errorCount += 1;
      result += "<li>" + shortError + "</li>";
    }

    var emailError = emailErrors(email);
    if (emailError != "None") {
      errorCount += 1;
      result += "<li>" + emailError + "</li>";
    }

    if (errorCount == 0) {
      result = "Good to Go! Copy the snippets below";
      div.className = "form-has-no-errors";
    } else {
      div.className = "form-has-errors";
    }
    div.innerHTML = result+"</ul>";
  }
</script>
<style type="text/css">
  #form-errors {
    margin: 30px 0px;
  }
  .form-has-errors {
    background-color: #F4CCCC;
  }
  .form-has-no-errors {
    background-color: #D9EAD3;
  }
</style>

<link href='http://fonts.googleapis.com/css?family=Open+Sans:400,300,600,700,800' rel='stylesheet' type='text/css'>

<form action="#">
  <div class="row">
    <input type="text" name="url-input" id="url-input" maxlength="500" onkeyup="changeContentText()" placeholder="eg: http://tuftscsx.com"/>
    <label id="url-input-label" for="url-input">url</label>
  </div>

  <div class="row">
    <input type="text" name="shorturl-input" id="shorturl-input" maxlength="500" onkeyup="changeContentText()" placeholder="eg: csx"/>
    <label id="shorturl-input-label" for="shorturl-input">Short url</label>
  </div>

  <div class="row">
    <input type="text" name="email-input" id="email-input" maxlength="500" onkeyup="changeContentText()" placeholder="At least 1 Tufts email"/>
    <label id="email-input-label" for="email-input">Email(s)</label>
  </div>

  <div class="row">
    <input type="text" name="description-input" id="description-input" maxlength="5000" onkeyup="changeContentText()" placeholder="(optional)"/>
    <label id="description-input-label" for="description-input">Description</label>
  </div>

  <div class="row">
    <input type="checkbox" name="is-hidden-checkbox" id="is-hidden-checkbox" onchange="changeContentText()"/>
    <label for="is-hidden-checkbox">Hide from front page</label>
  </div>
  <div id="form-errors"><br></div>
</form>



Copy Snippet A:

<div class="language-yaml highlighter-rouge"><pre class="highlight"><code id="content-title-text">0000-00-00-[please fill the input above].markdown</code></pre></div>

Copy Snippet B:

<div class="language-yaml highlighter-rouge"><pre class="highlight"><code id="content-body-text">---
layout: links
permalink: /:title
forward_to: http://[fill form above]
hidden: false
author: [fill form above]
---
[fill form above]
</code></pre></div>

Paste [here](https://github.com/TuftsCSX/go.tufts.io/new/master/_posts):

<img src="http://i.imgur.com/hhyUbHA.png" alt="">

___

### Making a Pull Request

1. Scroll to the bottom and hit "Propose New File"
2. Hit the big green "Create pull request" button
3. Add your name and tufts email in the box labeled "Leave a comment"
4. Hit the big green "Create pull request" button

And you're done! You'll have to wait a sec for us to approve the pull request, but feel free to ping me at richard@tufts.io

___

### Editing Links

(Must have a [Github](https://github.com/join) account)

1. Go to the [posts folder](https://github.com/TuftsCSX/go.tufts.io/tree/master/_posts)
2. Find your post, which is in the format `YYYY-MM-DD-<yoururl>.markdown`
3. Hit the pencil / edit button
4. Fork, change, pull request (same as creating a new link above)

___

## Why Github?

* We don't want to maintain a server, so we're basically using Github for authentication
* You can edit a link with another pull request
* Most people have github accounts, so they won't have to create another account on another website
* Encourages people to make a github account and get some commits under their belt
* Interface with TuftsCSX github page
* CSX admins don't have to learn a new interface
* Jekyll, the service we're using to serve static webpages, works amazingly well with Github and is crazy fast
