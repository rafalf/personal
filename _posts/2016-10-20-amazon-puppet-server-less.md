---
layout: post
title:  "Amazon instance provisioning: How to setup a masterless Puppet on Windows and apply manifests"
date:   2016-10-20
desc: "How to setup masterless puppet on Windows and apply manifests"
keywords: "amazon, aws, devops, puppet"
categories: [DevOps]
tags: [Amazon, AWS, DevOps, PowerShell, Puppet]
published: true
---


This post is about applying manifests on Windows with the Puppet in a masterless configuration. 
In a nutshell, Puppet is installed during instance bootstrap and then once instance is up and running puppet manifests are applied.

__When and why Puppet in the masterless configuration?__  
* No need to worry about certificates
* No need to look after the master node which could be another point of failure
* No need to update boxes frequently  

&nbsp;

Let's bring up the code ...

&nbsp;

### Step 1: Install puppet with Powershell

&nbsp;

```
Some code
  
```
&nbsp;


&nbsp;  

### Step 2: Run puppet apply 

&nbsp;  

```
Some code
```


