---
layout: post
title: "Selenium Cheatsheet"
comments: true
description: "A Cheatsheet on how to use selenium"
keywords: "selenium, automating, Cheatsheet"
---


### Basic

```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys

driver = webdriver.Firefox()
driver.get("http://www.python.org")
assert "Python" in driver.title
elem = driver.find_element_by_name("q")
elem.send_keys("pycon")
elem.send_keys(Keys.RETURN)
assert "No results found." not in driver.page_source
driver.back()
driver.close()
```

### Element

```python
# element html
element.get_attribute('innerHTML')
element.get_attribute('outerHTML')

# element text
element.text

# page html
page.source
```

### Forms

```python
# fill text element
element.send_keys("some text")
element.send_keys(" and some", Keys.ARROW_DOWN)
element.clear()

# select form
# http://selenium-python.readthedocs.org/navigating.html

# submit form
# Assume the button has the ID "submit" :)
driver.find_element_by_id("submit").click()
element.submit()
```

### Execute Js

```python
# run js
driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")
```

### Selector

```python
# http://selenium-python.readthedocs.org/locating-elements.html

# id
login_form = driver.find_element_by_id('loginForm')

# name
username = driver.find_element_by_name('username')

# xpath
username = driver.find_element_by_xpath("//form[input/@name='username']")

# css
content = driver.find_element_by_css_selector('p.content')

# link text
link1 = driver.find_element_by_link_text('Continue')
link2 = driver.find_element_by_partial_link_text('Conti')
```

### Wait

```python
# http://selenium-python.readthedocs.org/waits.html

###########################
#explicit wait
############################
from selenium.webdriver.support import expected_conditions as EC

wait = WebDriverWait(driver, 10)
element = wait.until(EC.element_to_be_clickable((By.ID,'someid')))

############################
# implicit wait
##########################
from selenium import webdriver
driver = webdriver.Firefox()
driver.implicitly_wait(10) # seconds
driver.get("http://somedomain/url_that_delays_loading")
myDynamicElement = driver.find_element_by_id("myDynamicElement")
```

The link to these cheatsheet can be found [here](https://gist.github.com/yoki/743f0f4489b85bcc5935be2bb166a99d).
