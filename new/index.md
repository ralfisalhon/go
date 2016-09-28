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
3. Open the [file creation page](https://github.com/TuftsCSX/go.tufts.io/new/master/_posts)
4. If you see "You need to fork this repository", fork the repository (new github accounts will need to verify your email)

___

### Content

Fill the form below and we'll generate the appropriate text for you to copy / past:

<section onload>
  <script type="text/javascript">
    var today = new Date();
    // var usedLinks = {};
    // function fetchUsedLinks() {
    //   var fs = require('fs');
    //   var files = fs.readdirSync('/posts/');
    //   console.log(files);
    // }
    // window.onload = fetchUsedLinks;

    function changeContentText() {
      var url = document.getElementById('website-url-input').value;
      var shorturl = document.getElementById('link-name-input').value;
      var email = document.getElementById('email-input').value;
      var desc = document.getElementById('description-input').value;
      var hidden = document.getElementById('is-hidden-checkbox').checked;

      var year = today.getFullYear();
      var month = today.getMonth();
      var day = today.getDay();

      if (month < 10) {
        month = "0" + month;
      };
      if (day < 10) {
        day = "0" + day
      };

      document.getElementById('content-title-text').innerHTML = year+"-"+month+"-"+day+"-"+shorturl+".markdown";

      if (url.indexOf("://") == -1) {
        url = "http://"+url
      }

      var result = "---\nlayout: links\npermalink: /:title\nforward_to: " + url +"\nhidden: "+hidden+"\nauthor: " + email +"\n---\n"+desc;

      document.getElementById('content-body-text').innerHTML = result;
      showErrorMessages(url, shorturl, email);
    }

    function shorturlErrors(url) {
      if (url.indexOf(" ") !== -1) {
        return "Link name can't contain spaces";
      } else if (/^[a-z0-9\-]+$/.test(url) == false) {
        return "Links can only use letters, numbers, and -";
      } else {
        return "None";
      }
    }

    function emailErrors(email) {
      if (email.indexOf("@tufts.edu") == -1) {
        return "Must include a Tufts email";
      } else {
        return "None";
      }
    }

    function showErrorMessages(url, shorturl, email) {
      var emptyUrlError = "<li>Url required</li>";
      var emptyShortUrlError = "<li>Link name required</li>";
      var emptyEmailError = "<li>Author email required</li>";
      var result = "Errors:<ul style='margin-top:0px'>";
      var div = document.getElementById('form-errors');
      var errorCount = 0;

      if (url.length <= 7) {
        errorCount += 1;
        result += emptyUrlError;
      }

      if (shorturl.length == 0) {
        errorCount += 1;
        result += emptyShortUrlError;
      } else {
        var shortError = shorturlErrors(shorturl);
        if (shortError != "None") {
          errorCount += 1;
          result += "<li>" + shortError + "</li>";
        }
      }

      if (email.length == 0) {
        errorCount += 1;
        result += emptyEmailError;
      } else {
        var emailError = emailErrors(email);
        if (emailError != "None") {
          errorCount += 1;
          result += "<li>" + emailError + "</li>";
        }
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
    input[type="text"] {
      display: block;
      margin: 0px 0px 5px 0px;
      padding: 0px 0px 0px 10px;
      width: 80%;
      font-family: sans-serif;
      font-size: 18px;
      appearance: none;
      box-shadow: none;
      border-radius: none;
    }
    input[type="text"]:focus {
      outline: none;
    }
    .form-has-errors {
      background-color: #F4CCCC;
    }
    .form-has-no-errors {
      background-color: #D9EAD3;
    }
  </style>
  <input id="website-url-input" maxlength="500" type="text" placeholder="Website url (eg: tuftscsx.com)*" onkeyup="changeContentText()">
  <input id="link-name-input" maxlength="500" type="text" placeholder="Short link name (eg: csx)*" onkeyup="changeContentText()">
  <input id="email-input" maxlength="100" type="text" placeholder="Tufts email*" onkeyup="changeContentText()">
  <input id="description-input" maxlength="5000" type="text" placeholder="description (optional)" onkeyup="changeContentText()">
  <input id="is-hidden-checkbox" type="checkbox" name="is-hidden" value="hidden" onchange="changeContentText()"> Hide from front page <br>
  <div id="form-errors"><br></div>
</section>

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

## Why Github?

* We don't want to maintain a server, so we're basically using Github for authentication
* You can edit a link with another pull request
* Most people have github accounts, so they won't have to create another account on another website
* Encourages people to make a github account and get some commits under their belt
* Interface with TuftsCSX github page
* CSX admins don't have to learn a new interface
* Jekyll, the service we're using to serve static webpages, works amazingly well with Github and is crazy fast
