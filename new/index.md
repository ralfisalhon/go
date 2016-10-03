---
layout: page
title: Creating a GO Link
description: "Instructions on how to install and customize the modern Jekyll theme HPSTR."
image:
  feature: abstract-11.jpg
modified: 2016-10-01
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
        }
        changeContentText();
      }
    }
  </script>
</head>

### First time?

Setup a [Github](https://github.com/join) account if you don't have one.  Make sure your [email is verified](https://help.github.com/articles/verifying-your-email-address/).

___

To make a link, you're going to make a really small file on github that we'll generate for you.  All you have to do is fill in the boxes below and hit the button.

**1) Fill the form below:**

<script type="text/javascript">
  var today = new Date();

  function changeContentText() {
    var url = document.getElementById('url-input').value;
    var shorturl = document.getElementById('shorturl-input').value;
    var email = document.getElementById('email-input').value;
    var desc = document.getElementById('description-input').value;
    var hidden = document.getElementById('is-hidden-checkbox').checked;
    var isProject = document.getElementById('is-project-checkbox').checked;

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
    var bodyText = "---\nlayout: links\npermalink: /:title\nforward_to: " + url +"\nauthor: " + email +"\nhidden: " + hidden +"\nproject: " + isProject +"\ndescription: " + desc + "\n---\n";
    var bodyText = encodeURIComponent(bodyText);
    var errorCount = showErrorMessages(url, shorturl, email);
    setCreatButtonLink(errorCount, fileName, bodyText, shorturl, email, desc);
  }

  function emailErrors(email) {
    if (email.length == 0) {
      return "Tufts email required";
    } else if (email.indexOf("@tufts.edu") == -1 && email.indexOf("@tufts.io") == -1) {
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
      result = "<b>2) Good to Go! Click the button below:</b>";
      div.className = "form-has-no-errors";
    } else {
      div.className = "form-has-errors";
    }
    div.innerHTML = result+"</ul>";
    return errorCount;
  }

  function setCreatButtonLink(errorCount, fileName, bodyText, shorturl, email, description) {
    var button = document.getElementById('create-link-button');
    var base = "https://github.com/TuftsCSX/go.tufts.io/new/master?filename=_posts/";
    if (errorCount == 0) {
      button.className = "btn btn-info";
      button.innerHTML = "Click to create new link";
      button.href = base + fileName + "&value=" + bodyText + "&message=Creating /" + shorturl + " by " + email + "&description=" + description;
      button.target = "_blank";
    } else {
      button.className = "btn btn-danger";
      button.innerHTML = "Please fix the errors above"
      button.href = "#short-url-generator";
      button.target = "";
    }
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

<form action="#" id="short-url-generator">
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
    <label for="is-hidden-checkbox">Hide from <a href="http://go.tufts.io">go.tufts.io</a> front page</label>
  </div>
  <div class="row">
    <input type="checkbox" name="is-project-checkbox" id="is-project-checkbox" onchange="changeContentText()"/>
    <label for="is-project-checkbox">Add to Tufts Projects? (<a href="http://go.tufts.io/projects">go.tufts.io/projects</a>)</label>
  </div>
  <div id="form-errors"><br></div>
</form>

<a id="create-link-button" href="https://github.com/TuftsCSX/go.tufts.io/new/master/_posts" class="btn" target="_blank">Click Me!</a>

**3) Now hit all the green buttons to make a pull request.**

Screenshots: [Fork Repository](http://imgur.com/qqACnUc.png)\* -> [Propose New File](http://imgur.com/jg67WRl.png) -> [Create pull request](http://imgur.com/fomzGmd.png) -> [Create pull request](http://imgur.com/62kmbe4.png)

And you're done! You'll have to wait a sec for us to approve the pull request, but feel free to ping me at richard@tufts.io

\* Only happens the first time

___

## Questions

### Editing Links
0. (Must have a [Github](https://github.com/join) account)
0. Go to the [posts folder](https://github.com/TuftsCSX/go.tufts.io/tree/master/_posts)
0. Find your post, which is in the format `YYYY-MM-DD-<yoururl>.markdown`
0. Hit the pencil / edit button
0. Fork, change, pull request (same as creating a new link above)

### Why Github?

0. We don't want to maintain a server, so we're basically using Github for authentication
0. You can edit a link with another pull request
0. Most people have github accounts, so they won't have to create another account on another website
0. Encourages people to make a github account and get some commits under their belt
0. Interface with TuftsCSX github page
0. CSX admins don't have to learn a new interface
0. Jekyll, the service we're using to serve static webpages, works amazingly well with Github and is crazy fast

### Help
0. [richard@tufts.io](mailto:richard@tufts.io) 617 435 6357
0. General tufts.io team: [team@tufts.io](mailto:team@tufts.io)
