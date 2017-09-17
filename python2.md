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

---

## 함수(function)

#### 매개변수(parameter)와 인자(argument)의 차이

함수 내부에서 함수에게 전달되어 온 변수는 매개변수라 부르며, 함수를 호출할 때 전달하는 변수는 인자로 부른다.

```python
# 함수 정의때는 매개변수
def func(매개변수1, 매개변수2):
  ...
  
# 함수 호출시에는 인자
>>> func(인자1, 인자2)
```

#### 리턴값이 없을 경우

함수에서 리턴해 주는 값이 없을 경우, 아무것도 없다는 뜻을 가진 `None`객체를 얻는다.

#### 기본 매개변수값 지정

인자가 제공되지 않을 경우, 기본 매개변수로 사용할 값을 지정할 수 있다.

```python
>>> def student(name, age, gender, cls='WPS'):
...   return {'name': name, 'age': age, 'gender': gender, 'class': cls}
... 
>>> student('hanyeong.lee', 30, 'male')
{'name': 'hanyeong.lee', 'age': 30, 'gender': 'male', 'class': 'WPS'}
```

#### 기본 매개변수값의 정의 시점

> 기본 매개변수값은 함수가 실행될 때 마다 계산되지 않고, 함수가 정의되는 시점에 계산되어 계속해서 사용된다.

```python
>>> def return_list(value, result=[]):
...   result.append(value)
...   return result
... 
>>> return_list('apple')
['apple']
>>> return_list('banana')
['apple', 'banana']
```

함수가 실행되는 시점에 기본 매개변수값을 계산하기 위해, 아래와 같이 바꿔준다.

```python
>>> def return_list(value, result=None):
...   if result is None:
...     result = []
...   result.append(value)
...   return result
... 
>>> return_list('apple')
['apple']
>>> return_list('banana')
['banana']
```

#### 위치인자 묶음

함수에 위치인자로 주어진 변수들의 묶음은 `*매개변수명`으로 사용할 수 있다.  
관용적으로 `*args`를 사용한다.

```python
def print_args(*args):
  print(args)
```

#### 키워드인자 묶음

함수에 키워드인자로 주어진 변수들의 묶음은 `**매개변수명`으로 사용할 수 있다.
관용적으로 `**kwargs`를 사용한다.

```python
def print_kwargs(**kwargs):
  print(kwargs)
```

#### 스코프(영역)

로컬 스코프에서 글로벌 스코프의 변수를 변경해야 한다면 , `global <변수이름>` 으로 해당 변수가 로컬 스코프에서 생성되는 것이 아닌 글로벌 영역에 이미 존재하는 값을 사용함을 명시해 주어야 한다.<br><br>

로컬 스코프 내부에 또 다른 로컬 스코프가 존재할 수 있다.<br>
전역 스코프가 아닌, 자신의 바로 바깥 영역의 로컬 스코프(자신보다 한 단계 위의 로컬 스코프)의 데이터를 참조하고자 한다면, `nonlocal <변수이름>` 키워드를 사용한다. 참고로 `nonlocal` 키워드는 `python 3`에서 추가된 내용이다.

### 클로져(Closure)

함수가 정의된 환경을 말하며, 파이썬 파일이 여러개일 경우 각 파일은 하나의 `모듈`역할을 하고, 각 `모듈`은 독립적인 환경을 가진다.  
독립된 환경은 각자의 영역을 전역 영역으로 사용한다.

#### 내부함수의 클로져

```python
>>> level = 0
>>> def outter():
...   level = 50
...   def inner():
...     nonlocal level
...     level += 3
...     print(level)
...   return inner
...
>>> f1 = outter()
>>> f2 = outter()
>>> f1()
53
>>> f1()
56
>>> f2()
53
```

#### 데코레이터 (decorator)

함수를 받아 다른 함수를 반환하는 함수. 예를 들면, 기존에 존재하던 함수를 바꾸지 않고 전달된 인자를 보기위한 디버깅 `print`함수를 추가한다던가 하는 기능을 할 수 있다.
<br><br>
여러 함수에 어떠한 특정한 기능을 모두 추가하고자 할 때 유용하다.

```python
def print_org_type(f):
    def ret_function(*args):
        for arg in args:
            print('%s type: %s' % (arg, type(arg)))
        return f(*args)
    return ret_function
    
#위의 함수는 원래 함수에 for문 2줄의 기능을 추가해주는 함수이다.
#만약 for문 두줄이 없다면 위의 함수는 원래 함수를 그대로 출력하는 함수이다.
```

위의 데코레이터 함수의 사용법은 아래와 같다.

```python
@print_org_type
def print_string(str_):
    return str_
    
#위 함수의 실행결과는 다음과 같다

print_org_type(print_string)(str_)
```

#### 기타

```python
>>> a = [1,2,3,4]
>>> def change():
... 	a[0] = 5

>>> change()
>>> a
[5,2,3,4]
```

이러한 결과가 나타나는 정확한 이유 알아서 정리하기
	