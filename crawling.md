# 크롤링(Crawling)

크롤링 혹은 스크래이핑은 웹 페이지를 그대로 가져와서 거기서 데이터를 추출해 내는 행위이다. 크롤링하는 소프트웨어는 크롤러라고 부른다.

### 크롤링의 기본

```python
import requests

from bs4 import BeautifulSoup


url = 'http://some.thing
response = requests.get(url)
soup = BeautifulSoup(response.text, 'lxml')

soup.select_one('table.viewList')
```

데이터를 추출할 웹 페이지의 데이터를 `request.get`을 통해 받아온다.<br>
예제에서는 받아온 데이터를 `response`라는 변수에 담았다.<br><br>

`response.text`로 받아온 데이터 중 content만 뽑은 후 `BeautifulSoup`의 첫번째 인자로 넣어주고 두번째 인자로는 parser인 `lxml`을 넣어주어 `BeautifulSoup`의 객체를 만들어준다. <br>
이렇게 하면 `BeautifulSoup`에서 content를 `lxml`을 이용, parsing 하여 탐색하기 쉬운 상태로 만들어준다.<br><br>

이렇게 만들어진 객체를(여기서는 `soup`이라는 변수) 여러가지 `BeautifulSoup`의 메서드를 이용해 탐색하여 볼 수 있다. 예제에서는 `BeautifulSoup`의 메서드 중 하나인 `select_one`메서드를 이용해 탐색을 했다.

탐색을 통해 원하는 데이터를 가져올 수 있다.

---

### Pickle

데이터를 저장하고 불러올 때 사용하는 내장함수이다.<br>

물론 `write()`와 `read()`를 이용해 데이터 입출력이 가능하지만, `pickle()`함수는 데이터를 원형 그대로 저장했다가 꺼내오는 것이 편리하다.<br>

```python
#pickle을 이용한 데이터 저장
pickle.dump(<저장할 내용>,open('저장할 위치', 'wb'))

#pickle을 이용한 데이터 로드
pickle.load(open('저장된 위치','rb'))
```

`pickle()`함수에서는 이진 데이터로 저장하고 불러와야 한다.

---

### BeautifulSoup

**BeautifulSoup** 는 HTML과 XML 파일에서 데이터를 추출하기 위한 파이썬 라이브러리로 이 도구는 파서 트리를 탐색, 검색 및 수정하는 관용적인 방법을 제공하기 위해 자주 사용하는 파서와 함께 작동한다.<br><br>

**BeautifulSoup** 의 자세한 내용은 다음 링크를 참조.<br>

https://www.crummy.com/software/BeautifulSoup/bs4/doc/ 

---

### Requests

**Requests** 의 자세한 내용은 다음 링크를 참조. <br>

http://docs.python-requests.org/en/master/

---

### Urlparse

내장함수인 `urlparse`를 이용하여 특정 **url** 을 분해하여 원하는 정보를 가져올 수도 있다.

---

### Crawling 활용

위의 내용을 응용해서 네이버 웹툰을 가져올 수 있는 crawler를 만듦(로그인 인증문제 해결 안돼서 19금 웹툰은 긁어오기 불가능).

[이 링크](https://github.com/darkblank/crawler)의 `crawler2.py` `episode.py` `utils.py` `/html`에 해당.