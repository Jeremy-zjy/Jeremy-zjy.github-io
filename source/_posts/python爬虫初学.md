---
title: python爬虫初学
date: 2019-02-09 17:44:38
tags:
---
#coding:utf-8
<!-- more -->
#author:Ericam_
## 代码
```
import re
import sys
from bs4 import BeautifulSoup
import urllib.request
import time
headers = ('User-Agent', 'Mozilla/5.0 (iPhone; CPU iPhone OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Version/9.0 Mobile/13B143 Safari/601.1')
opener = urllib.request.build_opener()
opener.addheaders = {headers}
urllib.request.install_opener(opener)
def get_download(url):
    file = urllib.request.urlopen(url)
    data = BeautifulSoup(file , from_encoding="utf8")    
    section_name = data.title.string
    print(section_name)
    section_text = data.select('#content #left font')[0].text
    section_text=re.sub( '\s+', '\r\n\t', section_text).strip('\r\n')
    fp = open("D:/python/2.txt",'a',encoding='utf-8')   
    fp.write(section_name+'\n')  
    fp.write(section_text+'\n')  
    fp.close()

if __name__ == '__main__':
    url = "http://www.net767.com/shuji/fubaba/10995.html"
    while(True):
        file = urllib.request.urlopen(url)
        data = BeautifulSoup(file , from_encoding="utf8")    
        section_name = data.title.string
        print(section_name)
        section_text = data.select('#content #left font')[0].text
        section_text=re.sub( '\s+', '\r\n\t', section_text).strip('\r\n')
        print(section_text)
        txt_section=data.select('#pagebar a')
        l1=len(txt_section)
        for num in range(1,l1-1):
            y=txt_section[num]['href']
            url = "http://www.net767.com"+y
            get_download(url)
            print(y)
        txt2_section=data.select('.LinkNextArticle')
        y2=txt2_section[0]['href']
        url = "http://www.net767.com"+y2
        if(url == 'http://www.net767.com/shuji/fubaba/11003_9.html'):
            break
        print(y2)
```
