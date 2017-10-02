# Python

수업 내용 중 새로운 내용, 어려운 내용 위주로 정리

## 05.문자열

### 문자열 나누기(split)

문자열의 내장함수 **split**을 사용<br>
**split**함수에 인자로 주어진 **구분자**를 기준으로 하나의 문자열을 리스트 형태로 반환해준다.

```
>>> girlsday = "민아,유라,소진,혜리"
>>> girlsday.split(',')
['민아', '유라', '소진', '혜리']

>>> girlsday = "민아 유라 소진 혜리"
>>> girlsday.split(' ')
['민아', '유라,' '소진', '혜리]
```

### 문자열 결합(join)

**split** 함수와 반대의 역할을 한다.<br>
문자열 리스트를 하나의 문자열로 결합해주며, 각 문자열을 결합해 줄 구분자 문자열을 지정한 후 **join**함수를 사용해준다.

```
>>> girlsday = ['민아','유라','소진','혜리']
>>> ', '.join(girlsday)
'민아, 유라, 소진, 혜리'

>>>' '.join(girlsday)
'민아 유라 소진 혜리'
```

### 문자열 포맷

#### 옛 스타일 (%)

```
string % data
```

변환타입|설명
---|---
%s	|	문자열
%d	|	10진수
%x	|	16진수
%o	|	8진수
%f	|	10진 부동소수점수
%e	|	지수로 나타낸 부동소수점수
%g	|	10진 부동소수점수 혹은 지수로 나타낸 부동소수점수
%%	|	리터럴 %

```
>>> '%s' % 42
'42'
>>> '%d x %d : %d' % (3, 4, 12)
'3 x 4 : 12'
```

#### 정렬

```
%[정렬기준(-,없음)][전체글자수].[문자길이 또는 소수점 이후 문자길이][변환타입]
```

```python
>>> d = 37
>>> f = 3.14
>>> s = 'Fastcampus'
>>> '%d %f %s' % (d, f, s)
'37 3.140000 Fastcampus'
>>> '%10d %10f %10s' % (d, f, s)
'        37   3.140000 Fastcampus'
>>> '%14d %14f %14s' % (d, f, s)
'            37       3.140000     Fastcampus'
>>> '%-14d %-14f %-14s' % (d, f, s)
'37             3.140000       Fastcampus    '
>>> '%-14.3d %-14.3f %-14.3s' % (d, f, s)
'037            3.140          Fas           '
```

#### 양쪽 공백 없애주기(strip)

```
#문자열 a의 양쪽 공백 없애기
a.strip()
```

#### 새 스타일 ({}, format)

```
{}.format(변수)
```

```python
# 기본형태
>>> '{} {} {}'.format(d, f, s)
'37 3.14 Fastcampus'

# 각 인자의 순서를 지정
>>> '{1} {2} {0}'.format(d, f, s)
'3.14 Fastcampus 37'

# 각 인자에 이름을 지정
>>> '{d} {f} {s}'.format(d=50, f=1.432, s='WPS')
'50 1.432 WPS'

# 딕셔너리로부터 변수 할당
>>> dict = {'d': d, 'f': f, 's': s}
>>> '{0[d]} {0[f]} {0[s]} {1}'.format(dict, 'WPS')
'37 3.14 Fastcampus WPS'

# 타입 지정자 입력
>>> '{:d} {:f} {:s}'.format(d, f, s)
'37 3.140000 Fastcampus'

# 이름과 타입지정자를 모두 사용
>>> '{digit:d} {float:f} {string:s}'.format(digit=700, float=1.4323, string='Welcome')
'700 1.432300 Welcome'

# 필드길이 10, 우측정렬
>>> '{:10d}'.format(d)
'        37'
>>> '{:>10d}'.format(d)
'        37'

# 필드길이 10, 좌측정렬
>>> '{:<10d}'.format(d)
'37        '

# 필드길이 10, 가운데 정렬
>>> '{:^10d}'.format(d)
'    37    '

# 필드길이 10, 가운데 정렬, 빈 공간은 ~로 채움
>>> '{:~^10d}'.format(d)
'~~~~37~~~~'
```

#### 가장 최근 버전  문자열 포맷

```python
#다음과 같이 쓸 수 있다
f'문자열{변수}'

#예제
>>>a = 'hi'
>>> f'{a}'
'hi'
```

---

## 06. 시퀀스

### 리스트

리스트는 순차적인 데이터를 나타내는 데 유용하며, 문자열과는 달리 내부 항목을 변경할 수 있다.

#### 리스트의 생성

```
>>> empty_list1 = []
>>> empty_list2 = list()
>>> sample_list = ['a', 'b', 'c', 'd']
>>> sample_list2 = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
```

#### 다른 데이터를 리스트로 변환

**list** 함수를 사용

```python
>>> list('League of legends')
['L', 'e', 'a', 'g', 'u', 'e', ' ', 'o', 'f', ' ', 'l', 'e', 'g', 'e', 'n', 'd', 's']
```

이 외에도 리스트로 변환 가능한 타입에서 사용가능하다.

#### 인덱스 연산

sample_list2를 이용해서 실습. 5월, 7월을 인덱스연산을 통해 추출해보자.

#### 내부항목 변경

sample_list를 이용, 3번째 요소인 'c'를 대문자 'C'로 바꿔본다.

#### 슬라이스 연산

- sample\_list2를 이용, 1월부터 3월씩 건너뛴 결과를 quarters에 할당
- sample\_list2를 이용, 끝에서부터 3번째 요소까지를 last_three에 할당
- sample\_list2를 이용, 끝에서부터 처음까지(거꾸로) 2월씩 건너뛴 결과를 reverse\_two\_steps에 할당

#### 리스트 항목 추가 (append)

```python
>>> sample_list.append('e')
>>> sample_list
['a', 'b', 'c', 'd', 'e']
```

#### 리스트 병합 (extend, +=)

```
>>> fruits = ['apple', 'banana', 'melon']
>>> colors = ['red', 'green', 'blue']
>>> fruits.extend(colors)
>>> fruits
['apple', 'banana', 'melon', 'red', 'green', 'blue']
```

```
>>> fruits = ['apple', 'banana', 'melon']
>>> colors = ['red', 'green', 'blue']
>>> fruits += colors
>>> fruits
['apple', 'banana', 'melon', 'red', 'green', 'blue']
```

**extend**대신 **append**를 사용하면?

#### 특정 위치에 리스트 항목 추가 (insert)


리스트 함수 **insert(offset)** 을 사용  


- fruits리스트의 1번째 위치에 'mango'를 추가해보자
- fruits리스트의 100번째 위치에 'pineapple'을 추가해보자

```
>>>fruits.insert(0, 'mango')
>>>fruits.insert(99, 'pineapple')
```

#### 특정 위치 리스트 항목 삭제 (del)

파이썬 구문 **del**을 사용  

> del은 리스트 함수가 아닌, 파이썬 구문이므로 `del <리스트>[오프셋]` 형식을 사용한다.

```
>>> del fruits[0]
```

#### 값으로 리스트 항목 삭제 (remove)

```
>>> fruits.remove('mango')
```

#### 리스트 항목 추출 후 삭제 (pop)

```
>>> fruits.pop()
>>> fruits.pop(-3)
```

#### 값으로 리스트 항목 오프셋 찾기 (index)

```
>>> fruits.index('red')
```

#### 존재여부 확인 (in)

```
>>> 'red' in fruits
True
```

#### 값 세기 (count)

```
>>> fruits.append('red')
>>> fruits.append('red')
>>> fruits.count('red')
3
```

#### 정렬하기 (sort, sorted)

- sort는 리스트 자체를 정렬
- sorted는 리스트의 정렬 복사본을 반환

#### 리스트 복사 (copy)


`L=['a', 'b', 'c']` 라는 리스트가 있다고 가정할 때 `L2=L`으로 `L2`도 `['a', 'b', 'c']`라는 리스트를 가리키게 할 수 있다. 하지만 여기서 `L`리스트 내부의 **'a'** 라는 값을 **'A'** 로 바꾸면 `L2` 리스트 내부의 **'a'** 라는 값도 **'A'** 로 바뀌게 된다. 이러한 현상을 방지하기 위한 것이 리스트 복사이다.


- copy함수 (ex. L2 = L.copy())
- list함수 (ex. L2 = list(L))
- 슬라이스 연산[:] (ex. L2 = L[:])

#### 언패킹 (unpacking)

N개의 요소를 가진 튜플이나 시퀀스를 N개나 그 이하의 요소로 나누려고 할 때 유용하다. 순환 가능한 모든 객체에 적용 가능하다.<br>
또한, 값의 치환에도 유용하게 쓰일 수 있다.

```
>>>colors = ['red', 'green', 'blue']
>>>f1, f2, f3 = colors
>>>f1
'red
>>>f2
'green'
>>>f3
'blue'
```

---

## 딕셔너리, 셋

### 딕셔너리(dictionary)

딕셔너리 내용은 대부분 알고 있어서 따로 정리 안함.

### 셋(set)

셋은 키만 있는 딕셔너리와 같으며, 중복된 값이 존재할 수 없다.

#### 셋 생성

```python
>>> empty_set = set()
>>> champions = {'lux', 'ahri', 'ezreal'}
```

#### 형변환

문자열, 리스트, 튜플, 딕셔너리를 셋으로 변환할 수 있으며, 중복된 값이 사라진다.

```
>>> set('ezreal')
{'e', 'z', 'a', 'l', 'r'}
```

```
>>>champion_dict = {
... 'Lux': 'the Lady of Luminosity',
... 'Ahri': 'the Nine-Tailed Fox',
... 'Ezreal': 'the Prodigal Explorer',
... 'Teemo': 'the Swift Scout',
... }
>>> set(champion_dict)
{'Ahri', 'Lux', 'Ezreal', 'Sona', 'Teemo'}
```

딕셔너리는 키만 남는다.

#### 집합 연산

연산자|설명
---|---
\|	|	합집합(Union)
&	|	교집합(Intersection)
\-	|	차집합(Difference)
^	|	대칭차집합(Exclusive)
<=	|	부분집합(Subset)
<	|	진부분집합(Proper subset)
\>=	|	상위집합(Superset)
\>	|	진상위집합(Proper superset)

```
>>> A = {1,2,3,4,5}
>>> B = {4,5,6,7,8,9}
>>> C = {4,5,6}
>>> A|B
>>> A&B
>>> A-B
>>> B-A
>>> A^B
>>> A <= B
>>> C <= B
>>> C < B
>>> B <= B
>>> B < B
```