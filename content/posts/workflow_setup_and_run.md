+++
title = "Workflow Setup and Run"
description = ""
featured_image = ""
date = 2019-03-01T23:54:43+08:00
categories = ["coding"]
tags = ["pipeline", "server", "DSL"]
comment = true
+++

Workflow

## Framework (Tools)

- Snakemake
- WDL
- nextflow
- CWL
- Martian (Pipeline Manager developed by 10x Genomics for Cellranger)
- make (GNU)

---

## Comparision

There are two types of workflow system.

- backward (pull) (output -> input)
  eg, make, snakemake

- forward (push) (input -> output)
  eg, nextflow, SciPipe
