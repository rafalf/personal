---
layout: post
title:  "OCR in Python"
date:   2016-10-30
desc: "Optical Character Recognition using Python"
keywords: "OCR, Python"
categories: [Automation]
tags: [Appium, Automation, Python, Android]
published: true
---


While automating an app for my freelance job on Android, I stumbled upon an issue which I had to get around.
In short, needed to verify Android toast messages which Appium due to the uiautomator limitations, cannot simply capture as of yet.
The solution was to use OCR which I found out was very straight forward in Python.

&nbsp;

## INSTALL THE TOOLS  

&nbsp;

### Step 1: Install Pillow  
`pip install Pillow`

### Step 2: Install tesseract-ocr  
[Download tesseratc-ocr from sourceforge](https://sourceforge.net/projects/tesseract-ocr-alt/files/) and install it. 

### Step 3: Install pytesseract
`pip install pytesseract` [pytesseract page](https://pypi.python.org/pypi/pytesseract/0.1)


and that's all we need. Easy, isn't it?

&nbsp;

## PYTHON CODE:

&nbsp;



```
import pytesseract
from PIL import Image, ImageEnhance, ImageFilter

pytesseract.pytesseract.tesseract_cmd = 'C:/Program Files (x86)/Tesseract-OCR/tesseract'

im = Image.open('C:\\Temp\\1.png')
im = im.convert('RGB') # convert to RGB
im.save('C:\\Temp\\1enh.png')

#im = Image.open("C:\\Temp\\1.png) # we could try to enhance
#im = im.filter(ImageFilter.MedianFilter())
#enhancer = ImageEnhance.Contrast(im)
#im = enhancer.enhance(2)
#im = im.convert('1')
#im.save('C:\\Temp\\1.png')

text = pytesseract.image_to_string(Image.open('C:\\Temp\\1.png'), lang="eng")
```