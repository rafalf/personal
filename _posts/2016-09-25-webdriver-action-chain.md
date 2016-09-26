---
layout: post
title:  "Webdriver - ActionChains routine"
date:   2016-09-23
desc: "Webdriver - ActionChains routine"
keywords: "webdriver"
categories: [Automation]
tags: [Webdriver, Automation, ActionChains]
published: true
---


ActionChains are to automate low level interactions: mouse movements, mouse hover, key press.
In my projects, I use it quiet frequently to interact with hidden elements on the page that are not displayed, Webdriver would throw an error when trying to access them but I want to perform an action e.g. click on it.
The routine for such an action is:

__Import__

```
from selenium.webdriver.common.action_chains import ActionChains
```

__Select Element__

that is a link on the page, hidden on H2 header and only seen when .fa-angle-down is clicked upon.

```
def select_element(self):
        
    selector = "#aS_Page .fa-angle-down" 
    down_item = WebDriverWait(self.driver, 10).until(lambda function: self.driver.find_element_by_css_selector(selector),
                    message='WebDriverWait timed out on selector:\n{0}'.format(selector))
    
    # expand element
    ActionChains(self.driver).move_to_element(down_item).perform()
    ActionChains(self.driver).move_to_element(down_item).click(down_item).perform()
            
    
    # wait until displays
    selector = "a[href$='/campaigns/create']"
    WebDriverWait(self.driver, 10).until(lambda function: self.driver.find_element_by_css_selector(selector).is_displayed(), 
                    message='WebDriverWait timed out on selector:\n{0}'.format(selector))
            
    item = WebDriverWait(self.driver, 10).until(lambda function: self.driver.find_element_by_css_selector(selector), 
                    message='WebDriverWait timed out on selector:\n{0}'.format(selector))
    
    # and the you can click on the element
    item.click()

```
     
