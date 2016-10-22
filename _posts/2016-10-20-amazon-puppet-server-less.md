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
In a nutshell, Puppet is installed during instance bootstrap ( Step 1 - Step 4) and then once instance is up and running Puppet manifests are applied (Step 5).

This post is written under the assumption that Puppet msi, modules and manifests are available on the instance, e.g. downloaded from s3 bucket prior to Puppet installation: [a short post about it](http://testprojects.co/devops/2016/10/04/amazon-s3-download.html) and manifests copied to C:\ProgramData\PuppetLabs\puppet\etc\modules


__When and why Puppet in the masterless configuration?__  
* Because we don't need to worry about certificates  
* Because we don't need to look after the master node which could be another point of failure  
* When we don't need to push updates frequently after boxes are configured  

&nbsp;



Let's bring up the code ...

&nbsp;

### Step 1: Install puppet with Powershell

&nbsp;

```
$msiArgumentList = "/qn /i puppet-enterprise-3.3.2.msi /l*v C:\install.log"
Start-Process -FilePath msiexec.exe -ArgumentList $msiArgumentList -Wait
  
```
&nbsp;


&nbsp;  

### Step 2: Add Puppet bin folder to the path and reload it 

&nbsp;  

```
$SetPath = $env:Path + ";C:\Program Files (x86)\Puppet Labs\Puppet Enterprise\bin\"
[Environment]::SetEnvironmentVariable("Path", "$SetPath", "Machine")
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
```

&nbsp;  

### Step 3: Install Puppet modules

&nbsp;  

```
$modules = @("joshcooper-powershell-0.0.6.tar.gz",
"puppetlabs-registry-1.0.0.tar.gz",
"rismoney-chocolatey-0.0.2.tar.gz"
)

foreach ($module in $modules) {
$module_command = "/c puppet module install --force " + $module + " --ignore-dependencies"
Start-Process -Wait "cmd.exe" -ArgumentList "$module_command" -RedirectStandardError temp.log
```

&nbsp;  

### Step 4: Disable Puppet agent service 

&nbsp;  

```
Set-Service pe-puppet -startuptype "disabled"
```

&nbsp;  

__We are all set up. Now we can apply puppet manifests__


### Step 5: Puppet apply 

&nbsp;  

```
puppet apply -v -l C:\manifest.log C:\ProgramData\PuppetLabs\puppet\etc\modules\manifest.pp
```


