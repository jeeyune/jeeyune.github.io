---
layout: post
title: Python 셀레니움을 이용한 간단한 페이스북 자동 로그인 프로그램 만들기
comments: true
categories: [Projects/Facebook_Auto_Login]
tags: [Python, Algorithm, Crawling, Selenium]
---

안녕하세요 오늘은 파이썬 셀레니움을 이용해 간단한 자동화 프로그램을 만들어 보려고 합니다!
<br><br>

**셀레니움 (Selenium) 이란?**
<br>
셀레니움은 웹 애플리케이션을 테스트 하는데 사용하는 오픈소스 (무료) 프레임워크 입니다.
셀레니움은 한개의 툴이 아닌 4가지 소프트웨어의 모음입니다.
<br>
- Selenium IDE (셀레니움 통합 개발 환경)
- Selenium RC (셀레니움 원격 제어)
- Web Driver
- Selenium Grid
<br>

셀레니움의 장점은 Web Driver API를 통해 OS에 설치된 크롬과 같은 브라우저를 제어 할 수 있기 때문에 비동기적인, 또는 뒤늦게 불러와지는 컨텐츠들을 크롤링해 가져올 수 있다는 점입니다.

<br><br>

# <span style="color:SeaGreen"> 1. 셀레니움 설치하기 </span>
<br>
셀레니움을 설치하기 위해서는 pip을 사용해야 합니다.
<br>
```
pip install selenium
```

만약 BS4가 설치가 안되어있다면 BS4 먼저 설치해주세요.
<br>
```
pip install beautifulsoup4
```
<br><br>

# <span style="color:SeaGreen"> 2. Facebook HTML 분석 </span>
<br>
페이스북의 로그인 페이지로 가서 개발자 모드를 살펴보면, 아이디와 비밀번호에 값을 입력하기 위해서는 id나 name같은 특정한 value를 알아야 합니다.
<br>
![facebook.JPG](/assets/img/facebook.JPG)
<br>

사진에서 보이듯이, 아이디를 입력하는 란은 'email', 비밀번호를 입력하는 란에는 'pass'라는 id를 사용하고 있네요.

<br>

# <span style="color:SeaGreen"> 2. 파이썬 코드 작성 </span>
<br>

```python
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.keys import keys

user = "아이디 저장"
pwd = "비밀번호 저장"

driver = webdriver.Chrome(ChromeDriverManager().install())      # 웹드라이버의 경로 입력
driver.get("http://facebook.com/")                              # Facebook 접속
assert "Facebook" in driver.title                               # driver.title이 Facebook이 맞는지 아닌지를 판단하기 위한 코드

elem = driver.find_element_by_id("email")                       # id가 email인 element를 찾아서 커서를 이동
elem.send_keys(user)                                            # user에 입력한 값을 커서가 있는 곳에 입력
elem = driver.find_element_by_id("pass")                        # 비밀번호도 같은방법으로 반복
elem.send_keys(pwd)
elem.send_keys(Keys.RETURN)                                     # 엔터키
```
<br>


위의 코드를 실행해보면, 자동으로 페이스북에 로그인이 되는 것을 확인 할 수 있습니다. 신기하죠? ㅎㅎ
<br>
다음엔 자동으로 로그인 한 후 타임라인에서 프로필을 긁어오는 프로그램을 구현해보도록 하겠습니다.

<br>
감사합니다!
