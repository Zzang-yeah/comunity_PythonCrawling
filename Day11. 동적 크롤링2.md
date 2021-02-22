# Day11. 동적 크롤링 2

## 크롤링 대상 사이트 살펴보기

동적 크롤링을 구현해서 나만의 번역 사전 만들기

https://papago.naver.com/

### 1. 동적 크롤링 진행 순서

> 파파고에 접속해서 번역하는 과정
>
> 1. 번역할 내용을 왼쪽 창에 입력
> 2. 번역 버튼 클릭
> 3. 번역 결과 수집

### 2. 필요한 요소의 태그 및 선택자 확인

- 번역 입력 칸 : <textarea id="txtSource">
- 번역 버튼 : <button id="btnTranslate">
- 번역 결과 칸 : <div id="txtTarget">

## 파이썬 코드 작성

```python
from selenium import webdriver
import time

driver = webdriver.Chrome('./chromedriver')

papago_url = 'https://papago.naver.com/'
driver.get(papago_url)
time.sleep(3)

question = input('번역할 영단어 입력 : ')

driver.find_element_by_css_selector('textarea#txtSource').send_keys(question)

driver.find_element_by_css_selector('button#btnTranslate').click()
time.sleep(1)

output = driver.find_element_by_css_selector('div#txtTarget').text
print('번역 결과 :', output)

driver.close()
```

## 나만의 번역 사전을 만들기 위한 코드 수정

```python
from selenium import webdriver
import time

my_dict = {}

driver = webdriver.Chrome('./chromedriver')

papago_url = 'https://papago.naver.com/'
driver.get(papago_url)
time.sleep(3)

num=int(input('번역할 영단어 갯수 입력 : '))
for i in range(num):
    question = input('번역할 영단어 입력 : ')
    driver.find_element_by_css_selector('textarea#txtSource').send_keys(question)
    driver.find_element_by_css_selector('button#btnTranslate').click()
    time.sleep(1)
    output = driver.find_element_by_css_selector('div#txtTarget').text
    my_dict[question] = output

    # 입력 칸 초기화
    driver.find_element_by_css_selector('textarea#txtSource').clear()

print(my_dict)

driver.close()
```

**✅ 오늘의 문제 : 동적크롤링 코드 작성하기**

오늘은 크롤링에 초점을 두지 않고, 파이썬 코딩에 초점을 둔 문제입니다.

정말 복잡한 사이트를 대상으로 크롤링을 하다 보면 소스코드가 1000줄이 넘어가는 경우도 발생합니다😂

그래서 크롤링이 복잡해질수록 소스코드를 더 깔끔하고 체계적으로 작성할 줄 알아야 한다고 생각합니다.

오늘의 문제는 **아래의 요구 사항**에 따라 진행해주시기 바랍니다!

**⭐ 조건 ⭐**

1. ```
   영단어 입력 - 번역 버튼 클릭 - 번역 결과 수집 - 입력 칸 초기화
   ```

    과정을 하나의 함수로 정의하기

   - 함수 이름 : get_papago_result
   - 입력 변수 : 1개 (영단어)
   - 리턴 값 : 번역 결과

2. 반복문을 활용하여 번역 5회 진행

3. 번역 사전 'my_dict' 출력

4. 소스코드 & 출력 결과 인증

👉 **코드 예시**

![Untitled1](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\Untitled1.png)

👉 **출력 예시**

![Untitled2](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\Untitled2.png)



```python
from selenium import webdriver
import time

my_dict = {}

driver = webdriver.Chrome('./chromedriver')

papago_url = 'https://papago.naver.com/'
driver.get(papago_url)
time.sleep(3)

def get_papago_result():
    global my_dict
    question = input('번역할 영단어 입력 : ')

    driver.find_element_by_css_selector('textarea#txtSource').send_keys(question)

    driver.find_element_by_css_selector('button#btnTranslate').click()
    time.sleep(1)

    output = driver.find_element_by_css_selector('div#txtTarget').text

    # 번역 사전에 저장 및 출력
    my_dict[question] = output

    driver.find_element_by_css_selector('textarea#txtSource').clear()

for i in range(5):
    get_papago_result()

print(my_dict)

driver.close()
```

출력결과

![image-20210223021555940](C:\Users\cat78\AppData\Roaming\Typora\typora-user-images\image-20210223021555940.png)