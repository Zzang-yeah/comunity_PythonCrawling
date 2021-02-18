# Day9. 정적 크롤링

## 파이썬 코드

코드의 기능

1)여러 페이지의 뉴스 기사 제목 수집

2)원하는 콘텐츠(키워드)입력받기

```python
#라이브러리 import
import requests
from bs4 import BeautifulSoup

#원하는 콘텐츠(키워드)입력받기
keyword = input("뉴스 검색 키워드: ")
#뉴스 기사마다 번호 붙이기
count = 0

#1~10페이지의 뉴스 기사 제목 수집
for page in range(1, 3):
    #키워드로 검색한 n번째 페이지
    news_url = 'https://search.hankyung.com/apps.frm/search.news?query=' + keyword + '&page=' + str(page)
    #페이지를 문자열 형태로 받아오기
    raw = requests.get(news_url)
    
    #html코드로 변환
    soup = BeautifulSoup(raw.text, 'html.parser')
    
    #뉴스 기사 제목 수집
    box = soup.find('ul', {'class' : 'article'})
    all_title = box.find_all('em', {'class': 'tit'})

    #출력
    for title in all_title:
        count += 1
        t = title.text
        print(count, '-', t.strip())
```

**✅ 오늘의 문제: 한국경제뉴스 크롤링**

오늘 실습을 통해 '전체뉴스'를 크롤링해보았죠!

이번 과제는 '한국경제뉴스'를 크롤링하는 것입니다😎

'한국경제뉴스'의 url 주소 패턴은 저번 시간의 문제를 풀며 확인하셨을거에요!

오늘의 문제는 **아래의 요구 사항**을 잘 따라서 진행해주시기 바랍니다!

**⭐ 조건 ⭐**

- '전체뉴스'가 아닌 '한국경제 뉴스' 크롤링
- 본인이 관심 있는 키워드를 input()으로 입력받기
- 출력 요소는 2개: 뉴스 기사 제목, 기사 작성 날짜 및 시간
- 1, 2페이지의 뉴스 20개만 출력
- 소스코드 및 출력 결과 인증

**👉 결과 예시 ⭐**

![img](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F2c34c03e-bcd8-4fda-ac50-2299da98250f%2FUntitled.png?table=block&id=c3bf1182-3457-4009-96b8-512a1bea6d5c&width=1150&userId=0bf67c59-da73-4d74-b499-88019e309008&cache=v2)

![img](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F53d5d8b6-c15e-4a60-8de1-6c2ab68a423e%2FUntitled.png?table=block&id=c95c8027-a968-49e1-b015-6d48b693fa58&width=2730&userId=0bf67c59-da73-4d74-b499-88019e309008&cache=v2)

**⭐ 힌트 ⭐**

- '전체뉴스'와 '한국경제뉴스'페이지의 동일한 요소 (기사 10개를 포함한 큰 틀, 기사 제목 등)들은 태그 및 선택자가 모두 동일합니다.
- 그렇다면 오늘의 코드에서 url 주소를 수정하고, '날짜 및 시간'을 출력하도록 수정하면 되겠죠?

```python
# 라이브러리 import
import requests
from bs4 import BeautifulSoup

# 원하는 콘텐츠(키워드)입력받기
keyword = input("뉴스 검색 키워드: ")
# 뉴스 기사마다 번호 붙이기
count = 0

# 1~10페이지의 뉴스 기사 제목 수집
for page in range(1, 3):
    # 키워드로 검색한 n번째 페이지
    news_url = 'https://search.hankyung.com/apps.frm/search.news?query=' + keyword + '&mediaid_clust=HKPAPER,HKCOM&page=' + str(page)
    # 페이지를 문자열 형태로 받아오기
    raw = requests.get(news_url)

    # html코드로 변환
    soup = BeautifulSoup(raw.text, 'html.parser')

    # 뉴스 기사 제목 수집
    box = soup.find('ul', {'class': 'article'})
    all_title = box.find_all('em', {'class': 'tit'})
    all_datetime=box.find_all('span', {'class':'date_time'})

    for i in range(10):
        count+=1
        t=all_title[i].text.strip()+' '+all_datetime[i].text.strip()
        print(count, '-', t)
```

