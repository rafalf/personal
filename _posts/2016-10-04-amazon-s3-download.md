---
layout: post
title:  "Amazon instance provisioning: Download zipped files from S3 bucket during instance boostrap with PowerShell"
date:   2016-10-04
desc: "A quick post about downloading and extracting resources from S3 bucket"
keywords: "amazon, aws, devops"
categories: [DevOps]
tags: [Amazon, AWS, DevOps, PowerShell]
published: true
---


This post is about downloading and extracting files from S3 bucket during instance bootstrap.
The process is carried out by injecting the user data script written in PowerShell 


### Step 1: Download from S3 bucket

&nbsp;

```
Write-Host "Download from s3 bucket" -nonewline -ForegroundColor Green
Read-S3Object -BucketName s3bucketName -Key downloadKey -File whereToDownload
  
```
&nbsp;

where:

__s3bucketName:__ bucket name to download from  
__downloadKey:__  file (key) to be downloaded  
__whereToDownload:__ destination directory   

__Example:__

```
Read-S3Object -BucketName PrepScripts -Key NewRelicServerMonitor.zip -File C:\PrepScripts
```

&nbsp;  

### Step 2: Extract 

&nbsp;  

```
Write-Host "Extract" -nonewline -ForegroundColor Green

$shell_app=new-object -com shell.application
$zip_file = $shell_app.namespace("C:\Prepscripts\NewRelicServerMonitor.zip")

#Set the destination directory for the extracts
$destination = $shell_app.namespace(C:\Prepscripts\Unpacked)

#unzip the files
$destination.Copyhere($zip_file.items())
```


