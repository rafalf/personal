---
layout: post
title:  "Webdriver: CSS - Locating Elements"
date:   2016-09-23
desc: "Webdriver: CSS - Locating Elements"
keywords: "css, webdriver"
categories: [Automation]
tags: [Webdriver, CSS, Automation]
published: true
---


Finding elements on the page and performing a given action on them, this is what webdriver does. So it's so important to be able to locate an unique element on the page to interract with. From my experience, best is to use __id(s)__, because there can be only one id with the given name on the page. Webdriver supports many different element locators: classes, names, links and partial links as well as css and xpaths. In this blog I'll show how to use css locators as I tend to use them a lot on projects. They are not as flexible as xpaths but they are significantly faster so between css and xpath, css is always my choice.
Consider the following page source:

&nbsp;

```
<a href="https://support.zendesk.com/hc/articles/article2094904">
    <div class="aH_icon whiteText">
        <i class="fa-before fa-lightbulb-o fa-5x"></i>
    </div>
    <header>
        <h2 id="centeredElement">What we do</h2>
    </header>
</a>
```

## To locate __a__ link element:  


### (sub-string matches )  
There are three special characters used:  
^ - starting text in the string   
$ - ending text in the string  
\* - containing text in the string  

&nbsp;

href starts with:

```
a[href^='https://support']
```

href ends with:

```
a[href$='https://article2094904']
```

href contains:

```
a[href*='support']
```

href equals:

```
a[href='https://support.zendesk.com/hc/articles/article2094904']
```


## To locate __h2__ heading  


### (sub-string matches )
```
[id^='centered']
```

&nbsp;
### by id - # (hash) stands for id

```
#centeredElement
```

### by class name - . (dot) stands for class name

```
.whiteText
```
```
.aH_icon
```

