---
layout: post
title:  "Webdriver & Python: A quick overview of ActionChains and Select"
date:   2016-09-23
desc: "Webdriver - ActionChains routine"
keywords: "webdriver"
categories: [Automation]
tags: [Webdriver, Automation, ActionChains, Python]
published: true
---


__ActionChains__ 

ActionChains are to automate low level interactions: mouse movements, mouse hover, key press.
However, I use them pretty frequently to interact with hidden elements on the page that are not displayed. 


Let's take a look at the following piece of code:

```

def select_element(self):
        
    selector = "#aS_Page .fa-angle-down" 
    down_item = WebDriverWait(self.driver, 10).until(lambda function: self.driver.find_element_by_css_selector(selector),
                    message='WebDriverWait timed out on selector:\n{0}'.format(selector))
    
    ActionChains(self.driver).move_to_element(down_item).perform()
    ActionChains(self.driver).move_to_element(down_item).click(down_item).perform()
            
    
    selector = "a[href$='/campaigns/create']"
    WebDriverWait(self.driver, 10).until(lambda function: self.driver.find_element_by_css_selector(selector).is_displayed(), 
                    message='WebDriverWait timed out on selector:\n{0}'.format(selector))
            
    item = WebDriverWait(self.driver, 10).until(lambda function: self.driver.find_element_by_css_selector(selector), 
                    message='WebDriverWait timed out on selector:\n{0}'.format(selector))
    
    item.click()

```


The above routine, expands the heading and clicks on the element that is not initally seen by webdriver.

I'll split it now into smaller pieces:

Find the element on the page, if .fa-angle-down is not found in 10 seconds, throw an error: WebDriverWait timed out on selector: followed by the locator 

```
selector = "#aS_Page .fa-angle-down" 
down_item = WebDriverWait(self.driver, 10).until(lambda function: self.driver.find_element_by_css_selector(selector))

```


Move the coursor to the element and expand it by clicking on it

```
ActionChains(self.driver).move_to_element(down_item).perform()
ActionChains(self.driver).move_to_element(down_item).click(down_item).perform()

```

The next lines make sure that the element is dislayed

```
.is_displayed()
```

and then once href is found, the element gets clicked


__Select__

Select is a class to perform operation on a Dropdown.


Consider the following code:


```
        
selector = "#Country"
item = Select(self.driver.find_element_by_css_selector(selector))
item.select_by_visible_text('Ireland')
            
```

As you can see, the first step is to locate the element with an id="Country", followed by the select by visible text operation. Webdriver supports other commands to perform a select, namely: select by index and value. 





     
