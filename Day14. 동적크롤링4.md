# Day14. 동적크롤링4

## 크롤링 대상 사이트 살펴보기

코뮤니티 카페에 접속해서 '신규회원게시판'에 작성된 게시물의 내용을 수집

1. 네이버 로그인
   1. 아이디 입력
   2. 비밀번호 입력
   3. 로그인 버튼 클릭

2. 코뮤니티 홈 접속
   1. 신규회원게시판 클릭
3. 신규회원게시판
   1. 첫번째 게시물 클릭

4. 게시물
   1. 글 내용의 태그 및 선택자 확인

## 파이썬 코드 작성

```python
from selenium import webdriver
import time

driver = webdriver.Chrome('./chromedriver')
login_url = 'https://nid.naver.com/nidlogin.login?mode=form&url=https%3A%2F%2Fwww.naver.com'
driver.get(login_url)
time.sleep(2)

my_id = 'comu'
my_pw = '12345'

driver.execute_script("document.getElementsByName('id')[0].value = \'" + my_id + "\'")
driver.execute_script("document.getElementsByName('pw')[0].value = \'" + my_pw + "\'")
time.sleep(1)

driver.find_element_by_id('log.login').click()
time.sleep(1)

comu_url = 'https://cafe.naver.com/codeuniv'
driver.get(comu_url)
time.sleep(1)

driver.find_element_by_id('menuLink90').click()
time.sleep(1)

driver.switch_to.frame('cafe_main')
time.sleep(1)

driver.find_element_by_xpath('//*[@id="main-area"]/div[4]/table/tbody/tr[1]/td[1]/div[2]/div/a').click()
time.sleep(1)

content = driver.find_element_by_css_selector('div.se-component-content').text
print(content)

driver.close()
```

**✅ 오늘의 문제 : 동적크롤링으로 코뮤니티 게시물 불러오기**

✔ `신규회원게시판`의 게시물 중 **가장 최근 게시물 20개**의 글 내용 출력하기

👉 **코드 예시**

![14-1](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\14-1.png)

👉 **출력 예시**

![14-2](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\14-2.png)

![14-3](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\14-3.png)

```python
from selenium import webdriver
import time

driver = webdriver.Chrome('./chromedriver')
login_url = 'https://nid.naver.com/nidlogin.login?mode=form&url=https%3A%2F%2Fwww.naver.com'
driver.get(login_url)
time.sleep(2)

my_id = 'comu'
my_pw = '12345'

driver.execute_script("document.getElementsByName('id')[0].value = \'" + my_id + "\'")
driver.execute_script("document.getElementsByName('pw')[0].value = \'" + my_pw + "\'")
time.sleep(1)

driver.find_element_by_id('log.login').click()
time.sleep(1)

comu_url = 'https://cafe.naver.com/codeuniv'
driver.get(comu_url)
time.sleep(1)

driver.find_element_by_id('menuLink90').click()
time.sleep(1)


driver.switch_to.frame('cafe_main')
time.sleep(1)

driver.find_element_by_xpath('//*[@id="main-area"]/div[4]/table/tbody/tr[1]/td[1]/div[2]/div/a').click()
time.sleep(1)

for i in range(1,21):
    content = driver.find_element_by_css_selector('div.se-component-content').text
    print('< '+str(i)+'번째 글 >')
    print(content)
    driver.find_element_by_css_selector('a.BaseButton.btn_next.BaseButton--skinGray.size_default').click()
    time.sleep(1)
    
driver.close()
```

![image-20210226011716157](C:\Users\cat78\AppData\Roaming\Typora\typora-user-images\image-20210226011716157.png)

![image-20210226011738033](C:\Users\cat78\AppData\Roaming\Typora\typora-user-images\image-20210226011738033.png)