+++
title = "How to Publish a Hugo Project to Remote Server Automatically?"
description = ""
featured_image = ""
date = 2018-03-03T16:21:39+08:00
categories = ["coding"]
tags = ["caddy", "net", "server"]
comment = true
+++

A pipeline for blogging automatically though Github

## Purpose

write and serve markdown blog without caring about the html, theme, archiving, server, website, domain ...

<!--more-->

## What to Build? (Workflow)

    Local repo
        ↓
    Github repo
        ↓
    Webhook
        ↓
    Server repo
        ↓
    Caddy hook
        ↓
    Hugo build
        ↓
    Caddy serve

## Step by Step Examples

1. generate a new hugo project

   ```bash
   # build a hugo site
   hugo new MyBlog
   # theme
   # git submodule
   # write the markdown file
   # vim content/posts/xxx.md
   ```

1. server side

   install `hugo, go, caddy`

1. github side

   webhook
