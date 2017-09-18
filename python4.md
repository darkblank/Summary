## 정규표현식(Regular Expressions)

특정한 패턴에 일치하는 복잡한 문자열을 처리할 때 사용하는 기법.

파이썬에서는 표준 모듈 `re`를 사용해서 정규표현식을 사용할 수 있다.

```python
import re

re.<함수명>(<패턴>, <문자열 소스>)
```

복잡하거나 자주 사용되는 패턴은 컴파일하여 사용할 수 있다.

```python
pattern1 = re.compile(<패턴>)
```

### match : 시작부분부터 일치하는 패턴 찾기

`match()`는 시작부분부터 일치하는 패턴만 찾는다.

매치 된다는 정보를 가진 `Match object`를 반환한다.
이 `Match object`를 가지고 두번째 처리가 가능하다.

### search : 첫 번째 일치하는 패턴 찾기

`search()` 는 처음으로 일치하는 패턴 하나를 찾아준다.

`Match object`를 반환한다.

### findall : 일치하는 모든 패턴 찾기

`findall()` 은 일치하는 모든 패턴을 찾아준다.

리스트를 반환한다.

### finditer : 일치하는 모든 패턴 찾기

`finditer()`는 `findall()`과 비슷하지만<br>
리스트를 반환하는 것이 아닌 `callable_iterater`라는 순회 가능한 객체를 반환한다. 이 객체를 **for문** 으로 순회시키면 `Match object`를 반환한다.

### split : 패턴으로 나누기

문자열의 `split()` 메서드와 비슷하지만 패턴을 사용할 수 있다.

### sub : 패턴 대체하기

문자열의 `replace()` 메서드와 비슷하지만 패턴을 사용할 수 있다.<br>
아래와 같이 사용한다.

```python
import re
re.sub(<대체되어질 패턴>, <대체할 패턴>, <문자열 소스>)
```
 
대체할 패턴 대신 함수를 이용할 수도 있다. 이러한 경우에는 새로운 함수를 정의하여 대체할 패턴 대신 함수명을 넣어준다.<br>
새로 정의한 함수에는 위치인자 1개( **match object** )가 들어가야 하며, 이 위치인자에는 대체되어질 패턴이 들어가게 된다.

아래에서 함수를 넣어 사용한 예를 볼 수 있다.

```python
In [1]: import re

In [2]: story = '''Born to the prestigious Crownguards, the paragon family of Demacian service, Luxanna was destined for greatness. She grew up as the family's only daughter, and she immediately took to the advanced education and lavish parties required of families as high profile as the Crownguards. As Lux matured, it became clear that she was extraordinarily gifted. She could play tricks that made people believe they had seen things that did not actually exist. She could also hide in plain sight. Somehow, she was able to reverse engineer arcane magical spells after seeing them cast only once. She was hailed as a prodigy, drawing the affections of the Demacian government, military, and citizens alike. As one of the youngest women to be tested by the College of Magic, she was discovered to possess a unique command over the powers of light. The young Lux viewed this as a great gift, something for her to embrace and use in the name of good. Realizing her unique skills, the Demacian military recruited and trained her in covert operations. She quickly became renowned for her daring achievements; the most dangerous of which found her deep in the chambers of the Noxian High Command. She extracted valuable inside information about the Noxus-Ionian conflict, earning her great favor with Demacians and Ionians alike. However, reconnaissance and surveillance was not for her. A light of her people, Lux's true calling was the League of Legends, where she could follow in her brother's footsteps and unleash her gifts as an inspiration for all of Demacia.'''

In [3]: p = re.compile(r'(?P<before>\w+)\s*,\s*(?P<after>\w+)')

In [4]: p
Out[4]: re.compile(r'(?P<before>\w+)\s*,\s*(?P<after>\w+)', re.UNICODE)

In [5]: def upper_first_group(m):
   ...:     return '{}, [{}]'.format(m.group(1).upper(), m.group(2))
   ...: 

In [6]: re.sub(p, upper_first_group, story)
Out[6]: "Born to the prestigious CROWNGUARDS, [the] paragon family of Demacian SERVICE, [Luxanna] was destined for greatness. She grew up as the family's only DAUGHTER, [and] she immediately took to the advanced education and lavish parties required of families as high profile as the Crownguards. As Lux MATURED, [it] became clear that she was extraordinarily gifted. She could play tricks that made people believe they had seen things that did not actually exist. She could also hide in plain sight. SOMEHOW, [she] was able to reverse engineer arcane magical spells after seeing them cast only once. She was hailed as a PRODIGY, [drawing] the affections of the Demacian GOVERNMENT, [military], and citizens alike.\n\nAs one of the youngest women to be tested by the College of MAGIC, [she] was discovered to possess a unique command over the powers of light. The young Lux viewed this as a great GIFT, [something] for her to embrace and use in the name of good. Realizing her unique SKILLS, [the] Demacian military recruited and trained her in covert operations. She quickly became renowned for her daring achievements; the most dangerous of which found her deep in the chambers of the Noxian High Command. She extracted valuable inside information about the Noxus-Ionian CONFLICT, [earning] her great favor with Demacians and Ionians alike. HOWEVER, [reconnaissance] and surveillance was not for her. A light of her PEOPLE, [Lux]'s true calling was the League of LEGENDS, [where] she could follow in her brother's footsteps and unleash her gifts as an inspiration for all of Demacia."

```

### 정규표현식의 패턴 문자

패턴|문자
---|---
\\d|숫자
\\D|비숫자
\\w|문자
\\W|비문자
\\s|공백 문자
\\S|비공백 문자
\\b|단어 경계 (\w와 \W의 경계)
\\B|비단어 경계

### 정규표현식의 패턴 지정자 (Pattern specifier)

**expr** 은 정규표현식을 말한다

패턴|의미
---|---
abc|리터럴 `abc`
(expr)|expr
expr1 \| expr2 | expr1 또는 expr2
`.` | `\n`을 제외한 모든 문자
`^` | 소스문자열의 시작
`$` | 소스문자열의 끝
expr`?` | 0 또는 1회의 expr
expr`*` | 0회 이상의 최대 expr
expr`*?`| 0회 이상의 최소 expr
expr`+` | 1회 이상의 최대 expr
expr`+?`| 1회 이상의 최소 expr
expr`{m}`| m회의 expr
expr`{m,n}`| m에서 n회의 최대 expr
expr`{m,n}?` | m에서 n회의 최소 expr
[abc] | a or b or c
[^abc] | not (a or b or c)
expr1(?=expr2) | 뒤에 expr2가 오면 expr1에 해당하는 부분
expr1(?!expr2) | 뒤에 expr2가 오지 않으면 expr1에 해당하는 부분
(?<=expr1)expr2 | 앞에 expr1이 오면 expr2에 해당하는 부분
(?<!expr1)expr2 | 앞에 expr1이 오지 않으면 expr2에 해당하는 부분

[점프 투 파이썬 - 정규표현식 (https://wikidocs.net/4309)](https://wikidocs.net/4309)

### 기타

`\`로 시작하는 패턴 문자나, 정규표현식에서 `\`를 직접 사용해야 하는 경우 문자열의 **이스케이프**문을 사용하지 않고, 정규식 내에서 `\`로 해석됨을 나타내기 위해 앞에 `r`을 붙인다 (raw string으로 취급된다)

정규표현식의 패턴에는 항상 앞에 `r`을 붙인다고 생각하는 것이 좋다. (만약 정규표현식 내부에서 `\`를 쓰지 않을 경우, `r`을 붙임과 붙이지 않음은 같은 결과를 가져온다)