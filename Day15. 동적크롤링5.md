# Day15. 동적크롤링5

## 크롤링 대상 사이트 살펴보기

뉴스 기사 본문 내용수집

1. 뉴스 기사 게시판

   1. 뉴스 기사 제목 클릭

2. 뉴스 기사 본문

3. 여러 개의 탭 다루기(뉴스 기사 게시판에서 뉴스 기사 제목 클릭하면 새로운 탭이 생기면서 뉴스 기사 본문을 보여줌)

   1. driver.window_handles 크롬 창에서 열린 탭을 모두 담고 있음

      ![15-1](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\15-1.png)

   2. driver.switch_to.window(작업할 탭)

      ```python
      # 1. 새로운 탭이 켜짐
      새로운 탭 등장!
      
      # 2. 'driver' 변수를 새로운 탭으로 전환
      driver.switch_to.window(driver.window_handles[-1])
      
      # 3. 새로운 탭에서 작업
      클릭, 값 입력, 내용 수집 등의 작업 수행
      
      # 4. 작업을 마치면 새로운 탭을 닫음
      driver.close()
      
      # 5. 다시 처음 탭으로 전환
      driver.switch_to.window(driver.window_handles[0])
      ```

## 파이썬 코드 작성

```python
from selenium import webdriver
import time

keyword = input('뉴스 검색 키워드 : ')

driver = webdriver.Chrome('./chromedriver')
news_url = 'https://search.hankyung.com/apps.frm/search.news?query=' + keyword + '&mediaid_clust=HKPAPER,HKCOM'
driver.get(news_url)
time.sleep(2)

ten_articles = driver.find_elements_by_css_selector('em.tit')

count = 0
for article in ten_articles:
    title = article.text

    article.click()
    time.sleep(1)

    driver.switch_to.window(driver.window_handles[-1])

    content = driver.find_element_by_id('articletxt').text
    seperate = content.split('\n')

    count += 1
    print(f'< {count}번 뉴스 - {title} >')
    for sep in seperate:
        if sep != '':
            print(sep, end = ' ')
    print('\n')

    driver.close()

    driver.switch_to_window(driver.window_handles[0])
    time.sleep(1)

driver.close()
```

**✅ 오늘의 문제 : 최신 30개의 뉴스 기사 본문 크롤링하기**

👉 **출력 예시**

![15-2](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\15-2.png)

![15-3](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\15-3.png)

![15-4](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\15-4.png)

```python
from selenium import webdriver
import time

keyword = input('뉴스 검색 키워드 : ')

driver = webdriver.Chrome('./chromedriver')
count = 0
for i in range(1,4):
    news_url = 'https://search.hankyung.com/apps.frm/search.news?query=' + keyword + '&mediaid_clust=HKPAPER,HKCOM&page='+str(i)
    driver.get(news_url)
    time.sleep(2)

    ten_articles = driver.find_elements_by_css_selector('em.tit')


    for article in ten_articles:
        title = article.text

        article.click()
        time.sleep(1)

        driver.switch_to.window(driver.window_handles[-1])

        content = driver.find_element_by_id('articletxt').text
        seperate = content.split('\n')

        count += 1
        print(f'< {count}번 뉴스 - {title} >')
        for sep in seperate:
            if sep != '':
                print(sep, end = ' ')
        print('\n')

        driver.close()

        driver.switch_to.window(driver.window_handles[0])
        time.sleep(1)

driver.close()
```

![15-5](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\15-5.PNG)

![15-6](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\15-6.PNG)