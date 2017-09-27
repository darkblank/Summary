# Django 기초

[Djangogirls](https://tutorial.djangogirls.org/ko/)를 참조하여 장고의 기초에 대해 알아본다.

이 페이지에서 진행하는 코드는 [Github 저장소](https://github.com/darkblank/djangogirls)에 올라가 있으므로 참고하도록 한다.

## Django 시작하기

[이 링크](https://github.com/darkblank/Summary/blob/master/Ready_for_Django.md)를 참조하여 Django를 시작하기 위한 환경을 구축한다.<br>
이 페이지에서는 환경 구축이 완료 된 이후부터 설명한다.

---

### 기본 설정 변경

`settings.py`에서 아래와 같이 변경하여 준다.

```python
TIME_ZONE = 'Asia/Seoul'
LANGUAGE_CODE = 'ko-kr'
``` 

### 데이터베이스 설정

Django는 기본적으로 sqlite3을 지원한다. `settings.py`를 보면 아래와 같은 내용이 있다. Djangogirls를 진행하는 동안은 이 데이터베이스를 사용하고 데이터베이스 변경법 등에 대해서는 나중에 알아보자.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

### 데이터베이스 생성

장고는 회원가입이나 로그인 등 기본적으로 제공하는 기능이 아주 많다. 이러한 기능들은 순수 코드로만 동작하는 것이 아니라 실제 데이터베이스가 있어야 작동을 한다. 따라서 기본 테이블을 미리 만들어 주어야 한다. 다음과 같은 명령어로 테이블을 생성한다.

```
#manage.py가 있는 위치에서
$python manage.py migrate

#또는
$./manage.py migrate
```

장고가 기본적으로 쓰는 테이블 개수만큼 데이터베이스에 테이블을 만들어준다. 그리고 이 테이블들의 정보는 `db.sqlite3`라는 파일에 기록이 된다. 앞으로 장고가 동작할 때는 이 파일 데이터베이스를 참조하게 된다. 