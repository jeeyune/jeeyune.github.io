---
layout: post
title: Python 크롤링을 이용한 IMAX 예매 알림봇 만들기 (1)
comments: true
categories: [Projects/IMAX_Notification_Bot]
tags: [Python, Crawling, Telegram, IMAX]
---

지난 4월, 한국에서 *'어벤져스: 엔드게임'* 의 아이맥스 티켓 예매전쟁은 정말 피 튀기는 **'피켓팅'** 이었다고 들었습니다.

일부 중고 거래 사이트에서 2만원 짜리 표가 11만 원 까지 올랐다고 하니 정말 어마어마한 인기를 끌었다는 걸 증명하는 것 같아요.

저도 영화를 정말 좋아하지만, 제게는 이 살인적인 예매경쟁에서 성공할 수 있는 금손이 없기에 이번 프로젝트를 진행하게 됐습니다.

#### 나같은 ~~💩손~~ 을 위한 보다 쉽게 아이맥스 영화를 예매할 수 있는 방법!

파이썬 크롤링을 통해 영화관 웹사이트에서 정보를 긁어 온 후, 일정한 간격으로 웹사이트를 확인 해 아이맥스 영화가 열린 시점에 바로 텔레그램 앱으로 알림을 받아 경쟁률이 높은 아이맥스 영화 티켓을 성공적으로 예매 할 수 있게 하는 것이 이 프로젝트의 목적입니다.

***

*텔레그램을 사용한 이유는?*

![compare.JPG](/assets/img/compare.JPG)
사진에서 확인할 수 있듯이, 개발자가 사용할 수 있는 외부 봇 플랫폼 중 가장 간단하기 때문입니다.

출처: [https://hanswsw.tistory.com/23](https://hanswsw.tistory.com/23)

<small>나중엔 더 업그레이드 시켜 카카오톡 채널로 만들어 보고 싶네요</small>

<br>
<br>
<br>


제가 이 프로젝트에서 크롤링 할 영화관 웹사이트는 바로 아이맥스관으로 유명한 용산CGV 입니다.

웹사이트 바로가기 : [http://www.cgv.co.kr/theaters/?areacode=01&theaterCode=0013](http://www.cgv.co.kr/theaters/?areacode=01&theaterCode=0013)


<br><br>

# <span style="color:SeaGreen"> 1. 크롤링 준비하기 </span>

크롤링에 필요한 모듈 2가지를 먼저 설치해야 합니다.

 - request
 - bs4 BeautifulSoup

이 모듈들을 설치하려면 Python 패키지 관리자인 pip을 사용해서 설치를 하시면 됩니다

<pre><code>
pip install requests bs4
</code></pre>

필요한 모듈이 몇 개 더 있지만 나중에 해당 포스트에서 다루도록 하겠습니다.

<br><br>

# <span style="color:SeaGreen"> 2. 상영시간표 크롤링하기 </span>

용산CGV 홈페이지로 가서 Chrome에서 제공하는 개발자 모드 (윈도우 : Ctrl + Shift + I / MAC : Cmd + Alt + I) 를 살펴보면,


![chrome_dev.JPG](/assets/img/chrome_dev.JPG)

이렇게 iframe 이라는 태그안에 또다른 URL이 있습니다.

iframe 태그는 현재 HTML 안에 또다른 다큐먼트를 넣을때 사용합니다.

src 에 있는 링크를 CGV 도메인 주소 뒤에 붙여넣기를 하게 되면

![iframe.JPG](/assets/img/iframe.JPG)

이런식으로 불필요한 요소 없이 오로지 상영시간표만 볼 수 있게 됩니다.

이제 해당 URL을 저장하고 requests 모듈로 페이지 정보를 받아오려면

<pre><code>
from requests

url = 'http://www.cgv.co.kr/common/showtimes/iframeTheater.aspx?areacode=01&theatercode=0013&date=20191125'
html = requests.get(url)
print(html.text)
</code></pre>

이렇게 코드를 작성해 주면 됩니다.

코드를 실행 해 보면, *우리가 원하는 정보가 아닌*  해당 URL **페이지 전체의 정보** 가 출력되기때문에 bs4를 통해 필요한 정보만 가져오도록 해야합니다.

다시 페이지로 돌아가서 개발자 도구를 열고,

![button.JPG](/assets/img/button.JPG)

위 사진에서 하이라이트 된 버튼을 클릭하게 되면 페이지에서 클릭한 부분의 HTML 태그를 찾아줍니다.

저 버튼을 클릭한 후,

![imax.JPG](/assets/img/imax.JPG)

페이지의 아이맥스 로고를 누르면 개발자 도구에서 해당하는 부분을 보여주게 되는데요

확인을 해보면 " span class='imax' " 라고 되어있는 것을 알 수 있습니다.

이 태그로 아이맥스 영화가 열렸는지에 대한 유무를 확인 할 수 있는데, 단순히 이 태그가 있으면 열린것, 없으면 열리지 않은 것이라고 판단 할 수 있습니다.

이제 bs4의 select 와 find_parent 메소드를 사용해서 코드를 써보면,

<pre><code>
import requests
from bs4 import BeautifulSoup

url = 'http://www.cgv.co.kr/common/showtimes/iframeTheater.aspx?areacode=01&theatercode=0013&date=20191125'


html = requests.get(url)
soup = BeautifulSoup(html.text, 'html.parser')
imax = soup.select('span.imax')
for item in imax:
    imax = item.find_parent('div', class_='col-times')
    title = imax.select_one('div.info-movie > a > strong').text.strip()
    print(title)
</code></pre>


soup 이라는 변수에 BeautifulSoup을 선언을 해주고

다시 imax 라는 변수에 soup.select를 이용해 'span.imax' 라는 값을 가진 모든 밸류를 imax에 저장합니다.

보통 아이맥스 영화관은 한 개지만, 저는 여러개일 경우도 생각해서 select_one 대신 select를 썼습니다.

그렇게되면 imax는 리스트가 되고, for loop으로 반복문을 넣어서 find_parent 메소드로 하나하나의 값의 부모를 찾아서 그 값의 영화 제목에 해당하는 태그를 select_one 으로 찾아 프린트를 하도록 했습니다.

코드를 실행해보면, 11월 25일자 아이맥스 예매 가능한 영화는 겨울왕국 2 입니다.



여기까지 requests 와 bs4를 사용해 크롤링을 해 보았구요 다음 포스트에는 코드 마무리와 텔레그램 봇 생성을 해보도록 하겠습니다.


읽어주셔서 감사합니다! 😊 
