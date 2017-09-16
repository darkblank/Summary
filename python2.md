## 제어문

### 조건표현식

```python
참일경우 if 조건식 else 거짓일 경우

>>>print('hi') if True else print('bye')
hi
```

조건표현식은 else일 경우 까지 다 써주어야 한다.<br>
중첩 조건표현식은 가독성이 떨어지므로 가급적이면 사용하지 않는다.<br>
컴프리헨션 뒤에 if문도 가능하다.

### for문 (조건에 따른 순회)

#### 중단하기 (break)

데이터를 순회하던 중, 특정 조건에서 순회를 멈추고 반복문을 빠져나갈 때 사용한다.

```python
for 항목 in iterable객체:
  (반복문을 중단하고 싶을때)break
```

#### 건너뛰기 (continue)

데이터를 순회하던 중, 반복문을 중단하지 않고 다음 반복으로 건너뛸 때 사용한다.

```python
for 항목 in iterable객체:
  (현재의 반복을 중간에 그만두고 다음 반복으로 건너뛰고 싶을 때)continue
```

#### break확인 (else)

for문으로 데이터를 순회하던 중, break문이 호출되지 않고 반복문이 종료되면 else문이 실행된다.

```python
for 항목 in iterable객체:
  pass
else:
  break가 한 번도 호출되지 않았을 경우의 코드
```

#### 여러 시퀀스 동시순회 (zip)

```python
>>> fruits = ['apple', 'banana', 'melon']
>>> colors = ['red', 'yellow', 'green', 'purple']
>>> for fruit, color in zip(fruits, colors):
...   print('fruit:', fruit, ' color:', color)
... 
fruit: apple  color: red
fruit: banana  color: yellow
fruit: melon  color: green
```

zip으로 묶은 시퀀스들 중, 가장 짧은 시퀀스가 완료되면 순회가 종료된다.

zip을 사용하면 여러 시퀀스로부터 튜플을 만들 수 있다.

```python
>>> list(zip(fruits, colors))
[('apple', 'red'), ('banana', 'yellow'), ('melon', 'green')]
```

zip으로 반환되는 것은 리스트가 아닌 zip클래스 형태의 iterable객체이기 때문에, 리스트 형태로 사용하려면 list()함수를 사용해준다.

dict()함수를 사용할 경우 딕셔너리 객체가 만들어지게 된다.

```python
dict(zip(fruits, colors))
{'apple': 'red', 'banana': 'yellow', 'melon': 'green'}
```

### 컴프리헨션(Comprehension)

>함축 또는 내포

iterable한 객체로부터 파이썬의 자료구조를 만드는 방법. 가독성과 사용성에서 이득을 얻을 수 있을 경우 항상 사용해준다.<br>
단, 2중 중첩을 넘어가면 일반적인 for문으로 표현하는것이 가독성이 좋다. 아니면 for문 안에 Comprehension을 사용하는 방법도 있다.

#### 리스트 컴프리헨션

```
[표현식 for 항목 in iterable객체]

>>>[x*2 for x in range(1,6)]
[2, 4, 6, 8, 10]
```

#### 리스트 컴프리헨션의 중첩

```
for color in colors:
	for fruit in fruits:
```

위 식을 다음과 같이 표현할 수 있다.

```
[(color, fruit) for color in colors for fruit in fruits]
```

 