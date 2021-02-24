# Day13. 동적크롤링3

## 구현할 소스코드1

영단어 번역 여러번 실행

번역 결과를 모두 'my_papago.csv'파일에 저장

```python
from selenium import webdriver
import time
import csv

driver = webdriver.Chrome('./chromedriver')
papago_url = 'https://papago.naver.com/'
driver.get(papago_url)
time.sleep(3)

f = open('./my_papago.csv', 'w', newline = '')
wtr = csv.writer(f)
wtr.writerow(['영단어', '번역결과'])

while True:
    keyword = input('번역할 영단어 입력 (0 입력하면 종료) : ')
    if keyword == '0':
        print('번역 종료')
        break

    driver.find_element_by_css_selector('textarea#txtSource').send_keys(keyword)
    driver.find_element_by_css_selector('button#btnTranslate').click()
    time.sleep(1)

    output = driver.find_element_by_css_selector('div#txtTarget').text
    
    wtr.writerow([keyword, output])
    
    driver.find_element_by_css_selector('textarea#txtSource').clear()

# 크롬 창 닫기
driver.close()

# 파일 닫기
f.close()
```

## 구현할 소스코드2

영단어 번역 여러번 실행

1)'my_papago.csv'파일에 있는 영단어일 경우, 저장하지 않음

2)'my_papago.csv'파일에 없는 영단어일 경우, 저장

```python
from selenium import webdriver
import time
import csv

driver = webdriver.Chrome('./chromedriver')
papago_url = 'https://papago.naver.com/'
driver.get(papago_url)
time.sleep(3)

f = open('./my_papago.csv', 'r')
rdr = csv.reader(f)
next(rdr)

my_dict = {}

for row in rdr:
    keyword = row[0]
    korean = row[1]
    my_dict[keyword] = korean

f.close()

f = open('./my_papago.csv', 'a', newline = '')
wtr = csv.writer(f)

while True:
    keyword = input('번역할 영단어 입력 (0 입력하면 종료) : ')
    if keyword == '0':
        print('번역 종료')
        break
    
    if keyword in my_dict.keys():
        print('이미 번역한 영단어입니다! 뜻은', my_dict[keyword], '입니다.')
    else:
        driver.find_element_by_css_selector('textarea#txtSource').send_keys(keyword)
        driver.find_element_by_css_selector('button#btnTranslate').click()
        time.sleep(1)

        output = driver.find_element_by_css_selector('div#txtTarget').text

        wtr.writerow([keyword, output])
				my_dict[keyword] = output

        driver.find_element_by_css_selector('textarea#txtSource').clear()

# 크롬 창 닫기
driver.close()

# 파일 닫기
f.close()
```

**✅ 오늘의 문제 : 한영사전 만들기**

✔ `**my_papago.csv` 에 저장된 번역 결과 (한국어)를 파파고에 입력해서 번역 결과 (영어)를 출력하기**

→ 파일 이름은 달라도 상관 없습니다!

![13-1](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\13-1.png)

앞서 우리가 해온 영어→한국어 번역이 잘 되었는지 확인하는 셈이죠😎

이번 문제는 반대로 한국어→영어 번역입니다.

⭐ **TIP** ⭐

1. 'my_papago.csv' 파일을 불러온 뒤, 리스트에 한글 번역 결과만 따로 저장해서 사용하세요!
2. 파파고 웹 페이지에 처음 접속한 순간, 어떤 버튼을 **딱 한번만 눌러주면** '영어' ↔ '한국어'가 가능합니다. 그 뒤로는 소스코드가 끝날 때까지 이 버튼을 다시 눌러줄 필요가 없습니다.
3. 나머지는 우리가 해온 것과 똑같습니다😉

👉 코드 예시

![13-2](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\13-2.png)

👉 출력 예시

![13-3](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\13-3.png)

![13-4](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\13-4.png)

```python
from selenium import webdriver
import time
import csv

driver = webdriver.Chrome('./chromedriver')
papago_url = 'https://papago.naver.com/'
driver.get(papago_url)
time.sleep(3)

f = open('./my_papago.csv', 'r')
rdr = csv.reader(f)
next(rdr)

hangul=[]
for row in rdr:
    hangul.append(row[1])
f.close()

f=open('./my_newpapago.csv', 'w', newline='')
wtr=csv.writer(f)
wtr.writerow(['영단어', '번역결과'])

for i in hangul:
    driver.find_element_by_css_selector('textarea#txtSource').send_keys(i)
    #driver.find_element_by_css_selector('button#btn_switch___x4Tcl disable___1r5H-').click()
    driver.find_element_by_css_selector('button#btnTranslate').click()
    time.sleep(1)

    output = driver.find_element_by_css_selector('div#txtTarget').text

    wtr.writerow([output, i])
    print(i+' : '+output)
    driver.find_element_by_css_selector('textarea#txtSource').clear()

# 크롬 창 닫기
driver.close()

# 파일 닫기
f.close()
```

