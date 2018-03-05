+++
title = "How to Publish a Hugo Project to Remote Server Automatically?"
date = 2018-03-03T16:21:39+08:00
tags = ["tech", "geek"]
categories = [""]
draft = false
+++

A pipeline for blogging automatically though Github

## Purpose

write and serve markdown blog without caring about the html, theme, archiving, server, website, domain ...

<!--more-->

## What to Build?

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
...

## Workflow

- generate a new hugo project

```bash
hugo new MyBlog
# git submodule
# theme
```

write the first markdown file

- server side

install `hugo, go, caddy`


- github side

webhook


