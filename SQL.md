# SQL

SQL 자습서<br>
https://www.w3schools.com/sql/default.asp

## SQL이란

데이터베이스를 액세스하고 조작하기 위한 표준언어

#### RDB

RDB(Relational Database)는 관계형 데이터 모델에 기초를 둔 데이터베이스이다. 관계형 데이터 모델이랑 데이터를 구성하는데 필요한 방법 중 하나로 모든 데이터를 2차원의 테이블 형태로 표현해준다.

#### RDBMS

RDBMS(Relational Database Management System)은 관계형 데이터베이스를 생성하고 수정하고 관리할 수 있는 소프트웨어이다.

## SQL 구문

데이터베이스에서 수행해야하는 대부분의 조치는 SQL 문으로 수행되어진다.
아래는 SELECT문의 예제이다.

```
#Customers 테이블의 모든 필드를 선택할 때

SELECT * FROM Customers;
```

구문은 항상 `;` 표시로 끝이나고<br>
SQL 키워드는 대소문자를 구분하지 않음.

### 자주 쓰이는 명령

SELECT - 데이터베이스에서 데이터를 추출한다.<br>
UPDATE - 데이터베이스의 데이터를 업데이트한다.<br>
DELETE - 데이터베이스에서 데이터를 삭제한다.<br>
INSERT INTO - 새로운 데이터를 데이터베이스에 삽입한다.<br>
CREATE DATABASE - 새 데이터베이스를 만든다.<br>
ALTER DATABASE - 데이터베이스를 수정한다.<br>
CREATE TABLE - 새 테이블을 만든다.<br>
ALTER TABLE - 테이블을 수정한다.<br>
DROP TABLE - 테이블을 삭제한다.<br>
CREATE INDEX - 색인(검색 키)를 작성한다.<br>
DROP INDEX - 색인을 삭제한다.

### SELECT

데이터베이스에서 데이터를 선택하는 데 사용되어진다. 

SELECT문의 예제는 위에서 다루었으므로 아래에서는 SELECT문의 옵션들에 대해서 살펴본다.

#### SELECT DISTINCT

중복 값을 제외한 값들만 나열하고 싶을 때 사용한다.

```python
#ex)Customer 테이블의 Country열에서 중복이 제거되어진 값을 나열
SELECT DISTINCT Country
FROM Customer;

#ex)Country열의 개수를 나열
SELECT COUNT(DISTINCT Country)
FROM Customers;
```

#### SELECT TOP

리턴 할 레코드 수를 정하는데 사용되어진다.

데이터베이스마다 문법이 다를 수 있으므로 상단의 홈페이지 링크를 참조하여 확인한다.

#### SELECT INTO

한 테이블의 데이터를 새 테이블로 복사한다.

```python
SELECT column1, column2, column3, ...
INTO newtable IN externaldb
FROM oldtable
WHERE condition;
```

위의 IN구문은 옵션이다. 다른 데이터베이스로 테이블을 복사할 때 사용되어진다.

---

### WHERE

WHERE 절은 지정된 조건을 충족하는 레코드만 추출하고 싶을 때 사용한다.

```python
#ex)Customers 테이블에서 Country가 Mexico인 데이터를 추출할 때
SELECT * FROM Customers
WHERE Country='Mexico';
```

#### WHERE 절에 있는 연산자

**Operator** | **Description**
---|---
= | Equal
<> | Not equal. Note: In some versions of SQL this operator may be written as !=
\> | Greater than
< | Less than
\>= | Greater than or equal
<= | Less than or equal
BETWEEN | Between an inclusive range
LIKE | Search for a pattern
IN | To specify multiple possible values for a column

#### AND OR NOT

WHERE 절은 AND, OR, NOT 연산자와의 결합도 가능하다.

#### IN

IN 연산자를 사용하여 WHERE 절에 여러 값을 지정할 수 있다.<br>
IN 연산자는 여러 OR 조건의 속기법이다.

```python
#ex)Customers테이블의 Country필드가 'Germany' 또는 'France' 또는 'UK' 인 모든 값
SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');
```

#### BETWEEN

주어진 범위 내의 값을 선택한다. 값은 숫자, 텍스트 또는 날짜 등이 될 수 있으며 시작값과 끝값이 포함되어진다.

```python
SELECT column_name
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

---

### ORDER BY

ORDER BY 문은 결과 집합을 오름차순 또는 내림차순으로 정렬하는데 사용된다. 기본적으로는 오름차순으로 정렬한다.

오름차순 : ASC(옵션 안주었을 시 기본값)<br>
내림차순 : DESC

```python
#ex)Customer 테이블의 모든 데이터를 Country열로 정렬 선택
SELECT * FROM Customers
ORDER BY Country;

#다음 예제는 위의 결과와 동일하다(오름차순)
SELECT * FROM Customers
ORDER BY Country ASC;

#ex)Customers테이블의 모든 데이터를 Country열로 내림차순 정렬 선택
SELECT * FROM Customers
ORDER BY Country DESC;

#ex)Customers 테이블의 모든 데이터를 Country열로 오름차순으로 정렬 후 CustomerName열로 내림차순 정렬 선택
SELECT * FORM Customers
ORDER BY Country ASC, CustomerName DESC;
```

---

### INSERT INTO

INSERT INTO문은 테이블에 새 레코드를 삽입하는 데 사용된다.

```python
#ex)Customers 테이블의 지정된 필드에만 데이터 삽입
INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```

#### INSERT INTO SELECT

한 테이블의 데이터를 복사하여 다른 테이블에 삽입할 때 사용되어진다.

소스 및 목표 테이블의 데이터 유형이 일치하여야 한다.

```python
INSERT INTO table2 (column1, column2, column3,...)
SELECT column1, column2, column3, ...
FROM table1
WHERE condition;
```

---

### NULL

NULL은 값이 없는 것을 의미한다. 이 것은 0이나 공백값이 있는 것과는 다른 것으로 값이 아예 지정이 되어있지 않은 것이다.

NULL값은 <이나 =같은 비교 연산자로 비교할 수 없고 대신 IS NULL 연산자와 IS NOT NULL 연산자를 사용해야 한다.

```python
#ex)IS NULL 구문의 예
SELECT column_names
FROM table_name
WHERE column_name IS NULL;
```

---

### UPDATE

기존의 레코드를 수정할 때 사용한다.

```python
#ex)Customer테이블의 CustomerID가 1인 레코드의 수정
UPDATE Customers
SET ContactName='Alfred Schmidt', City='Frankfurt'
WHERE CustomerID=1;
```

WHERE 절을 적지 않으면 모든 레코드의 ContactName과 City가 수정되어지므로 주의해야한다.

---

### DELETE

기존 레코드를 삭제할 때 사용된다.

```python
#ex)Customers 테이블의 특정 레코드 삭제하기
DELETE FROM Customers
WHERE CustomerName='Alfreds Futterkiste';

#ex)테이블 내의 모든 레코드 삭제하기
DELETE FROM table_name;
```

---

### Aggregate functions

#### MIN, MAX

선택된 필드의 가장 작은값 또는 가장 큰 값을 리턴한다.

```python
#ex)Products 테이블의 Price 중 가장 최저가격을 찾는다.
SELECT MIN(Price) AS SmallestPrice
FROM Products;
```

#### COUNT, AVG, SUM

COUNT() 함수는 지정된 기준과 일치하는 레코드의 개수를 반환한다.

AVG() 함수는 숫자 필드의 평균값을 반환한다.

SUM() 함수는 숫자 필드의 총 합계를 반환한다.

```python
#ex)COUNT()
SELECT COUNT(column_name)
FROM table_name
WHERE condition;

#ex)AVG()
SELECT AVG(column_name)
FROM table_name
WHERE condition;

#ex)SUM()
SELECT SUM(column_name)
FROM table_name
WHERE condition;
```

#### GROUP BY

aggregate functions와 함께 사용되어 결과 집합을 하나 이상의 열로 그룹화한다.

```python
#ex)Customers테이블에서 같은 Country를 갖고 있는 CustomerID의 수
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country;
```

#### HAVING

WHERE 이 aggregate functions와 함께 사용되어질 수 없어서 HAVING을 사용한다.

```python
#ex)Customers테이블에서 5명 이상의 CustmerID를 갖고 있는 Country만 나열
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;
```

---

### LIKE

WHERE 절에서 필드의 지정된 패턴을 검색하는 데 사용된다.

- % : 백분율 기호는 0, 1 또는 복수 문자를 나타낸다.
- _ : 밑줄은 문자 한개를 나타낸다.

AND 또는 OR 연산자를 사용하여 여러 조건의 결합도 가능하다.

```python
#ex)Customers 테이블의 CustomerName필드에서 'a'로 시작하는 모든 값
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%';

#ex)Customers 테이블의 CustomerName필드에서 'a' 또는 'b'또는 'c'로 시작하는 모든 값
SELECT * FROM Customers
WHERE CustomerName LIKE '[a-c]%';
```

LIKE Operator | Description
---|---
WHERE CustomerName LIKE 'a%' | Finds any values that starts with 'a'
WHERE CustomerName LIKE '%a' | Finds any values that ends with 'a'
WHERE CustomerName LIKE '%or%' | Finds any values that have 'or' in any position
WHERE CUstomerName LIKE '_r%' | Finds any values that 'r' in the second position
WHERE CustomerName LIKE 'a_%_%' | Finds any values that start with 'a' and are at least 3 characters in length
WHERE ContactName LIKE 'a%o' | Finds any values that starts with 'a' and ends with 'o'

---

### Aliases

Aliases는 테이블 또는 테이블 필드에 임시 이름을 읽기 쉽게 지정하는 것에 사용된다. Aliases는 조회 기간 동안만 존재한다.

```python
SELECT coulumn_name AS alias_name
FROM table_name;

SELECT column_name
FROM table_name AS alias_name;
```

---

### JOIN

JOIN문은 2개 이상의 테이블을 관련되어진 필드를 기반으로 하여 결합시킨다.

#### INNER JOIN

INNER JOIN문은 2개 이상의 테이블에서 일치하는 값을 가진 레코드만 선택한다.

```python
SELECT column_names
FROM table1
INNER JOIN table2 ON table1.column_name = table2.column_name;
```

위 예제에서 만약 table1.column_name과 table2.column_name에서 일치하는 값이 없다면 어떠한 레코드도 선택되어지지 않는다.

#### LEFT JOIN

LEFT JOIN은 왼쪽 테이블의 모든 레코드와 오른쪽 테이블의 일치하는 값을 가진 레코드를 반환하며, 오른쪽 레코드에서 일치하는 값이 없다면 NULL 값이 나오게 된다.

```python
SELECT column_names
FROM table1
LEFT JOIN table2 ON table1.column_name = table2.column_name;
```

#### RIGHT JOIN

RIGHT JOIN은 LEFT JOIN과 반대의 결과를 가진다.

```python
SELECT column_names
FROM table1
RIGHT JOIN table2 ON table1.column_name = table2.column_name;
```

#### FULL OUTER JOIN

FULL OUTER JOIN은 왼쪽과 오른쪽 테이블의 모든 값을 반환한다.

```python
SELECT column_names
FROM table1
FULL OUTER JOIN table2 ON table1.column_name = table2.column_name;
```

#### SELF JOIN

SELF JOIN은 하나의 테이블을 두개의 테이블처럼 JOIN으로 조회하는 방법으로, 원하는 데이터들이 한 테이블에 들어있을 때 사용한다.

```python
SELECT column_names
FROM table1 T1, table1 T2
WHERE condition;
```

---

### UNION

두 개 이상의 SELECT문의 결과 집합을 결합하는 데 사용되는 연산자이다.

각 SELECT문은 같은 수의 열을 가져야 하며, 열은 유사한 데이터 타입을 가져야 한다. 또한, 각 SELECT문의 열은 같은 순서로 있어야 한다.

UNION 연산자는 기본적으로 중복값은 제외하고 선택한다. 따라서 중복값을 허용하려면 UNION ALL을 사용한다.

```python
SELECT column_names FROM table1
UNION
SELECT column_names FROM table2
```

---

### EXISTS

하위 쿼리의 레코드 존재 여부를 테스트하는 데 사용되어진다.<br>
하위 쿼리가 하나 이상의 레코드를 반환하면 true를 반환한다.

```python
SELECT column_names
FROM table_name
WHERE EXISTS
(SELECT column_name FROM table_name WHERE condition);
```

---

### ANY & ALL

ANY 연산자는 하위 쿼리 값 중 조건을 충족하는 값들이 있으면 true와 함께 반환한다.<br>
ALL 연산자는 모든 하위 쿼리 값이 조건을 충족하면 true와 함께 반환한다.

```python
#ex)ANY
SELECT column_names
FROM table_name
WHERE column_name operator ANY
(SELECT column_name FROM table_name WHERE condition);

#ex)ALL
SELECT collumn_names
FROM table_name
WHERE column_name operator ALL
(SELECT column_name FROM table_name WHERE condition);
```

---

### Comments

한 줄 주석은 `--`로 시작한다.

여러줄 주석은 `/*`로 시작하고 `*/`로 끝난다.