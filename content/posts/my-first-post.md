---
title: "My First Post in Cloud 9"
date: 2022-12-26T13:58:11Z
draft: false
slug: my-first-post-in-cloud9
---

Hugo is a popular static site generator. This tutorial will guide you through using AWS Cloud9
to create a Hugo website and develop against it using the cloud development environment. :)

The final step will be the set up a continuous integration pipeline using AWS Code Pipeline.

Note these steps will be similar for other cloud environments or your OS X laptop, but this
particular tutorial targets AWS Cloud9.

The steps described next appear in this screencast AWS Hugo Continuous Delivery.

**Step 1: Launch an AWS Cloud9 Environment**

Use the AWS Free Tier and a Cloud9 Environment with the defaults.

**Step2: Download the hugo binary and put it in your Cloud9 path.**


```
wget https://github.com/gohugoio/hugo/releases/download/v0.109.0/hugo_extended_0.109.0_Linux-64bit.tar.gz
```

Put this file in the `~/bin` directory:

```
tar xzvf hugo_<VERSION>.tar.gz
mkdir -p ~/bin
mv ~/environment/hugo . #assuming that you download this into ~/environment
which hugo
```

The output of which hugo should be something like:

```
ec2-user:~/environment $ which hugo
~/bin/hugo
```

Then run the command to check if is everything is correctly setup:

```
hugo version
```

**Step3: Make a hugo website locally and test it in Cloud9**

One great thing about hugo is that it just a go binary. It makes it simple to both develop and
deploy hugo sites. The following section derives from the official hugo quickstart guide.

A. Create a new repo in Github and clone it into your environment. Change into it via the `cd`
command. Add a ``.gitignore` file with the word public in it. This step will stop the public
directory from checking into the repo.

B. Create a new site using the following command: hugo new site quickstart

C. Add a theme (you could swap this part with any theme you want).

**Step4: Create a post**

To create a new blog post, type the following command:

```
hugo new posts/my-first-post.md
``` 

This post is easily editable inside of AWS Cloud9.

**Step5: Run Hugo locally in Cloud9**

![Config TCP Port](/static/tcp-port-config-screenshot.png)


