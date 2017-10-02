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

### SELECT DISTINCT

중복 값을 제외한 값들만 나열하고 싶을 때 사용한다.

```
#ex)Customer 테이블의 Country열에서 중복이 제거되어진 값을 나열
SELECT DISTINCT Country
FROM Customer;

#ex)Country열의 개수를 나열
SELECT COUNT(DISTINCT Country)
FROM Customers;
```

---

### WHERE

WHERE 절은 지정된 조건을 충족하는 레코드만 추출하고 싶을 때 사용한다.

```
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

---

### ORDER BY

ORDER BY 문은 결과 집합을 오름차순 또는 내림차순으로 정렬하는데 사용된다. 기본적으로는 오름차순으로 정렬한다.

오름차순 : ASC(옵션 안주었을 시 기본값)<br>
내림차순 : DESC

```
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

