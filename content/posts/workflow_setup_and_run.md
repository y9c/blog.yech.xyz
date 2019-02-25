+++
title = "Workflow Setup and Run"
date = 2019-03-01T23:54:43+08:00
tags = ["tech", "coding", "server"]
categories = ["geek"]
draft = true
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
