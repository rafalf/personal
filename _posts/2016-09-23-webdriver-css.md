---
layout: post
title:  "Webdriver - Find Elements with CSS Selectors"
date:   2016-09-23
desc: "Webdriver - Find Elements with CSS Selectors"
keywords: "css, webdriver"
categories: [Automation]
tags: [Webdriver, CSS, Automation]
published: true
---


## Code:

```
<a href="https://support.zendesk.com/hc/articles/article2094904">
<div class="aH_icon whiteText"><i class="fa-before fa-lightbulb-o fa-5x"></i></div>
<header><h2 id="centeredElement">What we do</h2></header></a>
```

## sub-string matches 


__Find a element__

href starts with:

```
a[href^='https://support']
```

href ends with:

```
a[href$='https://support']
```

href contains:

```
a[href*='https://support']
```

href equals:

```
a[href='https://support.zendesk.com/hc/articles/article2094904']
```

__Find h2 element__

```
[id^='centered']
```

## id and class name

__Find h2 by id__

```
#centeredElement
```

__Find div by class name__

```
.whiteText or .aH_icon
```

