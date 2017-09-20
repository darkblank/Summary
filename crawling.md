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

이렇게 만들어진 객체를(여기서는 `soup`이라는 변수) 여러가지 메서드를 이용해 탐색하여 볼 수 있다. 예제에서는 `BeautifulSoup`의 메서드 중 하나인 `select_one`메서드를 이용해 탐색을 했다.

---

### pickle?

not finished.

### BeautifulSoup

**BeautifulSoup** 는 HTML과 XML 파일에서 데이터를 추출하기 위한 파이썬 라이브러리로 이 도구는 파서 트리를 탐색, 검색 및 수정하는 관용적인 방법을 제공하기 위해 자주 사용하는 파서와 함께 작동한다.<br><br>

**BeautifulSoup** 의 자세한 내용은 다음 링크를 참조.<br><br>

https://www.crummy.com/software/BeautifulSoup/bs4/doc/ 

---

### Requests

**Requests** 의 자세한 내용은 다음 링크를 참조. <br><br>

http://docs.python-requests.org/en/master/