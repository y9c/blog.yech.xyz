+++
title = "Write Rcpp Package in Vim"
description = ""
featured_image = ""
date = 2020-03-22T00:11:50+08:00
categories = ["coding"]
tags = ["vim", "cpp", "ccls"]
comment = true
+++

Plenty of tutorials have been posted online for writing Rcpp packages in Rstudio,
but few tutorials mention developing R packages in vim.

After some attempt, I have figure out the solution by myself.

### install requirement

- Rcpp in R
- neovim (with coc.nvim)
- ccls
- clang

### set up a new project

```bash
R -e 'Rcpp::Rcpp.package.skeleton("mypackage")'
cd ./mypackage
```

### setup project

create ccls config file (`.ccls`) in the project, and fill it with the following settings.

```
clang
%c -std=c11
%cpp -std=c++2a
-I/home/yech/.local/lib/R-3.6/library/Rcpp/include/
-I/usr/include/R
```
