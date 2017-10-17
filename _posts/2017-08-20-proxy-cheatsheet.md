---
layout: post
title: "Proxy Cheatsheet For Scraping"
comments: true
description: "Proxy Cheatsheet For Scraping"
keywords: "python, cheatsheet, proxy, scraping, scrapping, BeautifulSoup, beautiful soup, beautiful-soup, bs4, BeautifulSoup4, scrape, scrapy, tor, the onion router, http, https, socks5, privoxy, selenium, browser proxy, requests, python3, ipify, polipo, browser agent, user agent, scrapy middleware, proxy middleware, proxy cheatsheet, firefox, chrome, cheatsheetsm proxies, theOnionRouter, TOR"
---

---

# Proxy Setup

### Install **Tor**

`sudo apt install tor`

Tor works on socks5 proxy, hence for those which do not support socks5, we will install Privoxy which will provide http proxy wrapper on Tor's socks5 proxy. This is used in Scrapy.

### Install **Privoxy**

`sudo apt-get install privoxy`

---

### Selenium

For **Selenium**, Proxy settings are follows:

Here, Directly Tor is being used by socks proxy. A new firefox profile is created with proxy.

```
import time
from selenium import webdriver

fp = webdriver.FirefoxProfile()
fp.set_preference('network.proxy.type', 1)
fp.set_preference('network.proxy.socks', '127.0.0.1')
fp.set_preference('network.proxy.socks_port', 9050)
driver = webdriver.Firefox(fp)

driver.get('https://api.ipify.org')
print(driver.find_element_by_tag_name('pre').text)
driver.get('https://check.torproject.org/')
time.sleep(3)
driver.quit()
```

---

### BeautifulSoup and Requests

For **BeautifulSoup and Requests**, Proxy settings are follows:

Just provide proxy url in each request you create.

```
proxies = {'http': 'socks5://127.0.0.1:9050',
           'https': 'socks5://127.0.0.1:9050'}

resp = r.get('https://api.ipify.org/').text
print('Original IP: ', resp)
resp = r.get('https://api.ipify.org/', proxies=proxies).text
print('Proxy IP: ', resp)
```

---

### Scrapy

For **Scrapy**, create a middleware to change user agent for every request and use proxy.

In **middlewares.py:**

```
import os
import random
from scrapy import signals
from scrapy.conf import settings


class RandomUserAgentMiddleware(object):

    def process_request(self, request, spider):
        ua = random.choice(settings.get('USER_AGENT_LIST'))
        if ua:
            request.headers.setdefault('User-Agent', ua)


class ProxyMiddleware(object):

    def process_request(self, request, spider):
        request.meta['proxy'] = settings.get('HTTP_PROXY')
```

In **settings.py:**

```
USER_AGENT_LIST = [
    'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/535.7 (KHTML, like Gecko) Chrome/16.0.912.36 Safari/535.7',
    'Mozilla/5.0 (Windows NT 6.2; Win64; x64; rv:16.0) Gecko/16.0 Firefox/16.0',
    'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_3) AppleWebKit/534.55.3 (KHTML, like Gecko) Version/5.1.3 Safari/534.53.10'
]
# proxy for polipo
# HTTP_PROXY = 'http://127.0.0.1:8123'
# proxy for privoxy
HTTP_PROXY = 'http://127.0.0.1:8118'

# Enable or disable downloader middlewares
DOWNLOADER_MIDDLEWARES = {
    'scraper_name.middlewares.RandomUserAgentMiddleware': 400,
    'scraper_name.middlewares.ProxyMiddleware': 410,
    'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None
}
```

Create a spider, **try_tor.py**, save it in spiders folder of your project and see if proxy is applied or not.

**try_tor.py**:

```
# -*- coding: utf-8 -*-
import time
import scrapy
import requests as r


class TryTorSpider(scrapy.Spider):
    name = 'try_tor'
    allowed_domains = ['check.torproject.org']
    start_urls = ['http://check.torproject.org/']

    def parse(self, response):
        print(response.css('.content').extract_first()) 
```


It's Output should contain: 

```
2017-08-18 17:22:12 [stdout] INFO:     <img src="/torcheck/img/tor-not.png" class="onion">
2017-08-18 17:22:12 [stdout] INFO: 
2017-08-18 17:22:12 [stdout] INFO:   <h1 class="not">
2017-08-18 17:22:12 [stdout] INFO: 
2017-08-18 17:22:12 [stdout] INFO:       Congratulations. This browser is configured to use Tor.
2017-08-18 17:22:12 [stdout] INFO: 
2017-08-18 17:22:12 [stdout] INFO:   </h1>
2017-08-18 17:22:12 [stdout] INFO:   <p>Your IP address appears to be:  <strong>185.170.41.8</strong></p>
2017-08-18 17:22:12 [stdout] INFO: 
2017-08-18 17:22:12 [stdout] INFO: 
2017-08-18 17:22:12 [stdout] INFO: 
2017-08-18 17:22:12 [stdout] INFO:           <p class="security">
2017-08-18 17:22:12 [stdout] INFO:             However, it does not appear to be Tor Browser.<br>
2017-08-18 17:22:12 [stdout] INFO:             <a href="https://www.torproject.org/download/download-easy.html">Click here to go to the download page</a>
2017-08-18 17:22:12 [stdout] INFO:           </p>
2017-08-18 17:22:12 [stdout] INFO: 
```

**Congratulations. This browser is configured to use Tor.**

This means Tor has been setup and use proxy for each request.
