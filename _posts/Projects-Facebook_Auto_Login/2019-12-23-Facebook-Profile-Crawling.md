---
layout: post
title: Python 셀레니움과 BS4를 이용한 페이스북 프로필 크롤링
comments: true
categories: [Projects/Automation]
tags: [Python, Automation, Crawling, Selenium, BS4]
---

안녕하세요! 이번 포스팅에서는 셀레니움과 BeautifulSoup를 이용해 간단한 페이스북 프로필을 가져오는 프로그램을 작성해보려고 합니다.
<br><br>

**셀레니움 (Selenium) vs 뷰티플수프 (BeautifulSoup) 의 장단점?**
<br><br>
*셀레니움*
 * 웹 애플리케이션을 자동화 테스트 하는데 사용하는 오픈소스 프레임워크.
 * 실제 브라우저 처럼 작동하기 때문에 자바스크립트나 다른 형태의 데이터를 가져오기 쉬움. 즉 편리하다
 * 조금 느린 편

<br>

*뷰티플수프*
 * 빠르게 배울 수 있고, 쉽다.
 * 문서화가 잘 되어있다.
 * 복잡한 페이지를 파싱할 때 보다 편리하다.

<br>

# <span style="color:SeaGreen"> 1. 필요한 라이브러리 / 프레임워크 불러오기 </span>
<br>
만약 셀레니움과 BS4가 설치되어있지 않다면, [저번 포스팅](https://jeeyune.github.io/projects/facebook_auto_login/2019/12/18/Facebook-Automatic-Login.html) 을 참고해서 설치해야 한다. <br>

```python
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.keys import Keys
from bs4 import BeautifulSoup
```

<br>


# <span style="color:SeaGreen"> 2. HTML 분석 </span>

```python
# accessing personal profile using xpath
a = driver.find_elements_by_xpath('//*[@id="u_0_a"]/div[1]/div[1]/div/a')      # 프로필에 해당하는 태그를 찾아 우클릭 후 xpath 복사 후 붙여넣기
driver.get(a[0].get_attribute('href'))   # a의 첫번째 항목의 href 불러오기

req = driver.page_source

# parsing with bs4
soup = BeautifulSoup(req, 'html.parser')     # 페이지 소스 파싱

# load personal profile
information_list = soup.select('#intro_container_id')
for information in information_list:
    print(information.text)
```
<br>
# <span style="color:SeaGreen"> 3. 전체 코드 </span>

```python
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.keys import Keys
from bs4 import BeautifulSoup

# replace with your FB credentials
user = "id"
pwd = "password"

# accessing FB
driver = webdriver.Chrome(ChromeDriverManager().install())
driver.get("http://facebook.com/")
assert "Facebook" in driver.title

# login to FB
elem = driver.find_element_by_id("email")
elem.send_keys(user)
elem = driver.find_element_by_id("pass")
elem.send_keys(pwd)
elem.send_keys(Keys.RETURN)

# accessing personal profile using xpath
a = driver.find_elements_by_xpath('//*[@id="u_0_a"]/div[1]/div[1]/div/a')
driver.get(a[0].get_attribute('href'))

req = driver.page_source

# parsing with bs4
soup = BeautifulSoup(req, 'html.parser')

# load personal profile
information_list = soup.select('#intro_container_id')
for information in information_list:
    print(information.text)
```
