+++
title = "Download Data From Sra Through Google Cloud"
description = ""
featured_image = "https://www.gstatic.com/devrel-devsite/prod/v85bebc91899d0895957066f8f5069a9f78fae0477c52c06eb50e4921ab7d41ad/cloud/images/social-icon-google-cloud-1200-630.png"
date = 2022-02-07T23:05:21-06:00
categories = ["Bio"]
tags = ["linux", "google"]
comment = true
+++

> How to download NCBI SRA (Sequence Read Archive) data through Google Cloud (GCP)?

In some cases, you might need to download the orignal file from SRA, instead of downloading the data in `*.sra` format.

- You need the `*.bam` or `.*h5` format for 3rd generation sequencing data.
- You would like to have the orignal read name for the `*.fastq` format.

NCBI do not provide download link for the orignal files, but already stored the files on both Amazon Cloud (AWS) and Google Cloud. You can find the data link in the _Run Browser_ page.

Take dataset SRR13168868 as an example, you can have more details on page https://trace.ncbi.nlm.nih.gov/Traces/sra/?run=SRR13168868.
And Under _Data access_ tab, there are links startswith "gs://" or "s3://" prefix. The "gs://" one is from Google Cloud (GCP).

![cloud download links](/img/NCBI_cloud_download_links.png)

There is an [instruction page](https://www.ncbi.nlm.nih.gov/sra/docs/sra-cloud/) on NCBI, but it is to easy to follow, and do not provide command line demo.
There are some articles about how to download data from AWS, but very few about GCP. So I will only describe GCP.

1. A google cloud account is needed, and you might also need to complete the payment method.

2. On the linux server, download and install the `gcloud` package, with the `gsutil` command.

3. Don't forget to **login** the account.

```bash
gcloud auth login
```

If not, you will have an error mesage during the data download.

_...serviceusage.services.use access to the Google Cloud Project..._

4. Creat a key follow the instruction below.

https://cloud.google.com/iam/docs/creating-managing-service-account-keys

And download the key in json format

5. You can download the data link by command:

```bash
gsutil -m -u project_name cp gs://sra-pub-src-17/SRR13168867/HeLa_polyA_Input_rep1.R1.fastq.gz.1 ./
```

replace `project_name` in the command above into your own project name.
