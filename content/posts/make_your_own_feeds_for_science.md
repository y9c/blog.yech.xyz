+++
title = "Make Your Own Feeds for Science"
description = ""
featured_image = "https://user-images.githubusercontent.com/5415510/75457345-58af6b80-59b7-11ea-83f3-1642f00a656e.png"
date = 2020-02-27T02:20:22+08:00
categories = ["sci"]
tags = ["science", "RSS", "javascript", "community"]
comment = true
+++

The Internet is becoming more and more isolated and fragmented, but this has never been caused by technical issues.

Ironically, this phenomenon is particularly prominent in scientific journals, which is the exact opposite of the concept of openness and cooperation that science claims.
A scientist usually spend lots of time in visiting multiple websites for different scientific journals to follow the latest articles in a specific field.
An experienced scientist is often familiar with the layout of journal websites and keeps in mind the content style of different articles.
But all of this has nothing to do with science.

RSS is an old technology that allows users to access updates of a websites in a standardized format.
Contrary to various AI-based recommendation algorithms, this is a way for users to obtain information actively.
But due to considerations of income, RSS feed of major websites are not very useful, or even do not exist.

Since I became a freshman in college, I was a heavy user of [**Google Reader**](http://reader.google.com/).
Even within a few years after it closed, I opened its website occasionally to confirm whether it would reopen someday.
During that time, I started using **online services** like [Feed43](https://feed43.com/) and [FeedBurner](www.feedburner.com)
to write RSS rules for scientific journals.
At the same time, some Python crawlers are written and deployed locally to fetch the fulltext of some journals, and to generate **PDF-format magazines issue by issue**.

However, RSS rules need to be maintained in time with the revision of those websites.
As the task of wet experiments increases, some of the rules written by myself are outdated.
For many years I have conceived a community-driven RSS rule sharing platform.
Until one day I found that many people shared homemade RSS crawling rules on a platform called [RSShub](https://rsshub.app),
but there were no rules related to science.
Then I begun to rewrite my RSS rule into javascript code, and commit to RSShub repo.
It is still a on going process, but some of the rules are available now.
Such as:

- cover story and new issue notification

  - https://rsshub.app/cell/cover
  - https://rsshub.app/nature/cover
  - https://rsshub.app/sciencemag/cover

- news

  - https://rsshub.app/nature/news-and-comment/nature
  - https://rsshub.app/nature/news-and-comment/nbt
  - https://rsshub.app/nature/news-and-comment/neuro
  - https://rsshub.app/nature/news-and-comment/ng
  - https://rsshub.app/nature/news-and-comment/ni
  - https://rsshub.app/nature/news-and-comment/nmeth
  - https://rsshub.app/nature/news-and-comment/nchem
  - https://rsshub.app/nature/news-and-comment/nmat
  - https://rsshub.app/nature/news-and-comment/natmachintell

- papers

  - https://rsshub.app/nature/research/nbt
  - https://rsshub.app/nature/research/neuro
  - https://rsshub.app/nature/research/ng
  - https://rsshub.app/nature/research/ni
  - https://rsshub.app/nature/research/nmeth
  - https://rsshub.app/nature/research/nchem
  - https://rsshub.app/nature/research/nmat
  - https://rsshub.app/nature/research/natmachintell
  - https://rsshub.app/sciencemag/current/science
  - https://rsshub.app/sciencemag/current/advances
  - https://rsshub.app/sciencemag/current/immunology
  - https://rsshub.app/sciencemag/current/robotics
  - https://rsshub.app/sciencemag/current/stke
  - https://rsshub.app/sciencemag/current/stm
  - https://rsshub.app/cell/cell/current
