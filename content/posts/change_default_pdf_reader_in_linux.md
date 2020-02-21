+++
title = "Change Default pdf Reader in Linux"
description = ""
featured_image = ""
date = 2018-03-29T21:41:30+08:00
categories = ["coding"]
tags = ["website", "nodejs"]
comment = true
+++

> solve the problem that gimp open pdf as default

- check **filetype** of a certain file

  ```bash
  xdg-mime query filetype xxx.pdf
  ```

- check **default mimetype** of a certain filetype

  ```bash
  xdg-mime query default application/pdf
  ```

- set **default mimetype** for a certain filetype

  ```bash
  xdg-mime default evince.desktop application/pdf
  ```

> Reference:

- https://superuser.com/questions/170035/pdfs-open-in-gimp-on-linux-system
