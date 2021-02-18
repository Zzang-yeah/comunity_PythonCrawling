# Day8. 정적 크롤링

## 크롤링 대상 사이트 살펴보기

한국경제 사이트

url형태 : https://~~~~~?query=검색어&page=1

->한국 경제 사이트에서 '검색어'로 검색한 1페이지

## '뉴스 기사 제목'의 태그 및 선택자 확인

![image-20210218183046828](C:\Users\cat78\AppData\Roaming\Typora\typora-user-images\image-20210218183046828.png)

## 오늘의 문제

**⭐ 1번 문제**

**'전체뉴스'가 아닌 '한국경제뉴스'의 url 주소 패턴 파악**

https://search.hankyung.com/apps.frm/search.news?query=%EC%BD%94%EB%A1%9C%EB%82%98&mediaid_clust=HKPAPER,HKCOM&page=2

전체 뉴스와 다른점 mediaid clust=HKPAPER,HKCOM부분 추가

**⭐ 2번 문제**

**뉴스 기사의 '날짜 및 시간' 태그 파악**

![KakaoTalk_20210218_183914299](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\KakaoTalk_20210218_183914299.png)

![KakaoTalk_20210218_183925672](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\KakaoTalk_20210218_183925672.png)

![KakaoTalk_20210218_183932112](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\KakaoTalk_20210218_183932112.png)

![KakaoTalk_20210218_183938596](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\KakaoTalk_20210218_183938596.png)

![KakaoTalk_20210218_183949873](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\KakaoTalk_20210218_183949873.png)

![KakaoTalk_20210218_183955962](C:\Users\cat78\Desktop\대외활동\코뮤니티_파이썬크롤링2기\KakaoTalk_20210218_183955962.png)

div.section_count->ul.article->li->div.txt_wrap->p.info->span.date_time

