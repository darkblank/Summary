# Postgresql

### 설치법

```
$ sudo apt-get update
$ sudo apt-get install postgresql postgresql-contrib
```

---

### 새로운 계정 생성

```
# 다음 내용을 입력하여 서버의 postgres 계정으로 전환한다.
$ sudo -i -u postgres
# 이후 다음 내용을 입력하여 계정을 생성하여준다.
postgres@server:~$ createuser --interactive
```

계정 변경 없이 새로운 계정 생성을 위해서는 다음과 같이 할 수 있다.

```
$ sudo -u postgres createuser --interactive
```

여기서, 계정을 생성할 때는 ubuntu 계정과 같은 이름으로 생성하여 주도록 한다.

계정을 생성한 이후, 다음과 같이 입력하여 줌으로써 **postgres** 가 아닌 다른 계정으로 **postgresql** 을 이용할 수 있다.

```
$ sudo -i -u <생성한 계정 이름>
```

---

### 데이터베이스 생성

```
# 계정을 변환한 상태에서는
$ createdb <데이터베이스 이름>

# 계정 변환이 이루어지지 않은 상태에서는
$ sudo -u <계정 이름> createdb <데이터베이스 이름>
```

---

### 데이터베이스 다루기

```
# 계정 변환 상태에서는
$ psql <데이터베이스 이름>

# 계정 변환이 이루어지지 않은 상태에서는
$ sudo u <계정 이름> psql <데이터베이스 이름>
```