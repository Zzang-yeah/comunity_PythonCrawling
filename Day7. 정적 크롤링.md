# Day7. 정적 크롤링

## 라이브러리 BeautifulSoup

HTML문서를 탐색해서 원하는 부분만 쉽게 뽑아낼 수 있게 해주는 라이브러리

## BeautifulSoup의 필요성

저번시간에 requests로도 HTML코드를 불러왔었는데 그건 HTML 코드 자체를 출력한 게 아니라 텍스트 형태로 출력했을 뿐

크롤링을 위해서는 단순히 문자열을 다루는 게 아니라 실제 HTML코드를 다뤄야함!

BeautifulSoup은 실제 HTML코드로 변환

## BeautifulSoup 살펴보기

```python
from bs4 import BeautifulSoup
#from 라이브러리 import 메소드 : 해당 라이브러리에서 특정 메소드를 가져온다
```

```python
BeautifulSoup(문자열, 'html.parser')
#문자열을 HTML코드로 해석하여 읽어라
#문자열 위치에 requests로 읽어온 html코드(문자열)을 넣어주면 됨
```

```python
#find_all()

#1. 원하는 부분의 태그 1개 : <div id="example1">
#사용법 1. 태그이름사용
HTML코드.find_all('div')
#사용법 2. 선택자 정보 사용
HTML코드.find_all(id='example1')

#2. 원하는 부분의 태그 2개 : <div id="example1">, <span class="example2">
#사용법 1. 태그이름사용
HTML코드.find_all(['div', 'span'])
#사용법 2. 선택자 정보 사용
HTML코드.find_all(attrs = {'id':'example1','class':'example2'})
```

```python
#find()

#원하는 부분의 태그: <div id="example1">

#사용법 1. 태그 이름 사용 
(실제 HTML 코드).find('div')

#사용법 2. 선택자 정보 사용 
(실제 HTML 코드).find(id = 'example1')
(실제 HTML 코드).find(attrs = {'id':'example1'})

#사용법 3. 태그 이름과 선택자 정보 모두 사용
(실제 HTML 코드).find('div', {'id' : 'example1'})
```

## 파이썬 코드

```python
from bs4 import BeautifulSoup
import requests

lotto_url = 'https://dhlottery.co.kr/gameResult.do?method=byWin'
#lotto_url의 html코드를 문자열 형태로 받아옴
raw=requests.get(lotto_url)

#lotto_url의 html코드 문자열을 html코드 형태로 해석
soup=BeautifulSoup(raw.text, 'html.parser')

#lotto_url의 html코드 속에서 <div class='nums'>를 찾고
box=soup.find('div',{'class':'nums'})
#<span>태그를 가진 걸 다 찾음
numbers=box.find_all('span')

print('<최근 로또 당첨 번호>')
#numbers에는 <span>text</span>의 형태로 여러개가 리스트로 저장되어있음
#우리는 <span>태그는 필요없으므로 text데이터만 출력하도록 .text를 붙여줌
for number in numbers:
    print(number.text)
```

![image-20210217001505986](C:\Users\cat78\AppData\Roaming\Typora\typora-user-images\image-20210217001505986.png)