# Day6. 정적 크롤링

## 크롤링 대상 사이트 살펴보기

로또 당첨 번호를 크롤링해올 것

한페이지내에 필요한 정보가 모두 나와있으므로 정적 크롤링

```html


<div class="nums">
		<div>
				<strong> </strong>
				<p>
					<span> </span>
					<span> </span>
					<span> </span>
					<span> </span>
					<span> </span>
					<span> </span>
				</p>
		</div>
		<div>
				<strong> </strong>
				<p>
					<span> </span>
				</p>
		</div>
</div>
```

당첨 번호는 위의 코드내에 존재

## 라이브러리 'requests'

http와 관련된 작업을 편하게 할 수 있도록 해주는 라이브러리

웹페이지에 무언가의 작업 요청을 할 수 있는 클래스

## 웹사이트의 HTML불러오기

웹사이트의 html코드를 불러오기 위해 requests 라이브러리 사용

**requests.get('url 주소')** : 웹 페이지의 내용을 요청하는 함수

## 파이썬 코드

```python
import reuqests

lotto_url='로또당첨번호url'
raw=requests.get(lotto_url)
print(raw.text)
```

![img](https://cafeptthumb-phinf.pstatic.net/MjAyMTAyMTZfMTc2/MDAxNjEzNDMyMjQ0NTgx.WAHJDAsbpasSApthzHEqJMypH5qNy_dtJj73pMl7xo0g.e8OEYr3kHH-aZiMCUhq5cGxe4h6StY5rvSMY6NPMdC8g.PNG/image.png?type=w1600)

해당 웹페이지의 전체 html코드를 띄워준다