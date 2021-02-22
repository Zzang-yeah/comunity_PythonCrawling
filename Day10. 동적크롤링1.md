# Day10. 동적크롤링1

## 라이브러리 'selenium'

웹드라이버를 사용하여 자동화를 실현하는 라이브러리

사람이 데이터를 수집하는 방식 그대로 크롤링하는 기계를 만들어냄

속도는 느리지만 다양한 동작이 가능하기 때문에 한계가 거의 없음

## webdriver

selenium의 webdriver는 많은 브라우저, os및 프로그래밍 언어를 지원하며 웹 응용 프로그램들의 테스트를 단순화 및 가속화해주는 툴

장점

1. 다채로운 프로그래밍 언어 지원
2. 쉽고 단순한 사용법
3. 실행 과정의 시각화로 인한 실시간 확인

사용하는 브라우저에 맞게 설치해야함

크롬 브라우저를 사용할거라서 chromedriver.exe설치

## chromedriver.exe

selenium에서 명령을 보낼 때 크롬을 제어하는 방법 제공

버전 확인 자주 할 것

## 라이브러리 'time'

파이썬과 함께 자동으로 설치된 라이브러리라 별도의 설치과정은 X

sleep()을 자주 사용함->소스코드 진행 속도는 굉장히 빠른데에 비해 웹페이지의 로딩속도가 못 따라올 수 도 있어서 time.sleep(1)과 같이 1초 정도의 여유를 주면서 크롤링이 끊기지 않도록 함

## 동적 크롤링

```python
#비어있는 크롬창을 3초정도 띄웠다가 종료시키기
#라이브러리 import
from selenium import webdriver
import time

#webdriver에 chromedriver.exe를 연결한 객체를 생성
driver=webdriver.Chrome('./chromedriver')

#크롬창이 열리고 3초 정도의 여유주기
time.sleep(3)

#창 닫기
driver.close()
```

```python
#실제 웹페이지(ex.파파고) 크롬창을 3초정도 띄웠다가 종료시키기
#라이브러리 import
from selenium import webdriver
import time

#webdriver에 chromedriver.exe를 연결한 객체를 생성
driver=webdriver.Chrome('./chromedriver')
papago_url='https://papago.naver.com/'
driver.get(papago_url)

#크롬창이 열리고 3초 정도의 여유주기
time.sleep(3)

#창 닫기
driver.close()
```

## 'selenium' 내장 함수

1. get() : 입력한 url주소로 접속하는 함수
2. find_element_by_ == 정적크롤링의 find()
   - css_selector('태그 및 선택자') 
   - id(id이름)/class_name(class이름) 
   - xpath(xpath) : xpath는 xml문서의 특정 부분의 위치를 찾을 때 사용하는 언어

3. find_elements_by_ == 정적크롤링의 find_all()
4. click() : html요소를 클릭
5. send_keys('텍스트') : html 요소에 직접 텍스트 입력

## 오늘의 문제

✅ **오늘의 문제: 동적크롤링 이해하기**

오늘 크게 다섯 종류의 'selenium' 내장함수를 살펴보았는데요!

'동적크롤링에서 이런 것도 구현할 수 있을까?' 싶은 기능이 있다면 말씀해주세요!

만약 검색해서 실제로 그런 기능을 구현하는 내장함수가 있다면 함께 적어주시기 바랍니다😉

selenium과는 관계없지만 time.sleep()은 지정한 시간만큼 기다려야하는 게 비효율적이여보여서 로딩이 되면 자동으로 넘어가는 함수는 없나하고 찾아봤다. driver.implicitly_wait('기다릴 시간')을 사용하면 기다릴 시간 내에 로드가 되면 넘어가고 시간 내에 완료가 되지 않으면 에러를 띄우고 종료된다고 한다.