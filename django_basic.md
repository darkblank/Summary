# Django 기초

[Djangogirls](https://tutorial.djangogirls.org/ko/)를 참조하여 장고의 기초에 대해 알아본다.

이 페이지에서 진행하는 코드는 [Github 저장소](https://github.com/darkblank/djangogirls)에 올라가 있으므로 참고하도록 한다.

**장고 공식 홈페이지**<br>
https://docs.djangoproject.com/ko/1.11/

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

### 모델 생성

내부 애플리케이션에서 사용할 모든 모델 객체는 `models.py`에 선언하여 만들어 준다. 모델 객체는 데이터베이스랑 연결되어지는 객체이고 모델 객체를 정의할 때 `models.Model`를 상속받아 만든다. 이를 통해 장고가 데이터베이스와 연결되어지는 모델 객체임을 알게 된다. 이렇게 만들어진 모델 하나(클래스 하나)가 하나의 테이블이 된다.

### 데이터베이스에 모델 테이블 만들기

```
$python manage.py makemigrations
#또는
$python manage.py makemigrations <app 이름>
```

위 명령으로 모델의 변경사항에 대한 기록, 즉 migration 파일을 만들어준다. 이렇게 변경사항에 대한 기록을 파일로 만들어 줌으로써 여러가지 편의에 쓰일 수 있다. 위 기록을 실제로 데이터베이스에 적용하여 테이블을 생성하여 준다. 위에서도 한번 해보았던 명령인 `migrate`을 쓴다.

```
#manage.py가 있는 폴더에서
$python manage.py migrate
```


### 관리자 페이지

`models.py`에 생성한 모델을 `admin.py`에 등록하여 관리할 수 있다.

`admin.py`에 모델을 **import** 해 온 후 `admin.site.register(모델명)`으로 등록 해준다.

등록한 모델의 관리는 `/admin` 페이지에서 할 수 있다.

#### 관리자 생성

`$python manage.py createsuperuser`로 생성 가능하다.

생성되어진 관리자 아이디로 관리자 페이지에 로그인이 가능하다.

### 뷰 생성

뷰는 기본적으로 두가지 역할을 실행한다. 

하나는 모델에서 필요한 정보를 받아와서 템플릿에 전달하는 역할이다. 즉, 뷰와 템플릿 사이에서 데이터를 가공하는 역할이다. 이것이 Rendering이다

또 다른 역할은 urlresolver로 분석되어진 요청 URL을 받아 Rendering되어진 템플릿을 응답으로 리턴하는 것이다. 

뷰는 `views.py`에서 추가하여 줄 수 있다.

### 템플릿 생성

`views.py`에서 직접 html파일을 코드 안에 쓸 수도 있으나, 가독성이나 템플릿을 사용할 때가 여러가지 편리한점이 많기 때문에 템플릿을 따로 만든다. 

템플릿을 만들기 위해 장고 애플리케이션 폴더 아래에 **templates** 폴더를 생성하고(패키지가 아님) 하위폴더로 **내부 애플리케이션 폴더와 이름이 같은 폴더** 를 하나 더 생성하여준다(내부 애플리케이션에서 사용할 것이므로.) 그리고 그 하위폴더 내부에 html파일을 만들어서 쓴다.

우리가 만든 **templates** 폴더를 장고가 참조하게 하기 위해서 `settings.py`에 **TEMPLATE_DIR** 이라는 변수를 만들어 이 곳에 **templates** 폴더의 위치를 적어준다. 그리고 이 **TEMPLATE_DIR** 를 `settings.py`의 **TEMPLATES** 이라는 변수의 딕셔너리 안의 **DIR** 이라는 key의 value에 리스트 형태로 넣어준다. 이렇게 함으로써 템플릿을 사용할 때마다 파일 입출력을 통해 템플릿 파일의 위치를 찾는 수고를 덜 수 있다.

#### 템플릿 상속

장고에서는 템플릿 상속을 지원한다.

만약 중복되어지는 html파일이 많다면 중복되어지는 부분을 base템플릿으로 만든다. 내용이 바뀌게 될 부분만 아래처럼 템플릿 언어로 처리 한다.

```
{% block <이름> %}

{% endblock %}
```

base템플릿에 위처럼 템플릿 언어로 처리한 부분을 상속받을 템플릿에도 똑같이 써주고 **block** 태그 안에 바꾸어줄 내용을 html태그를 이용하여 적으면 된다. 템플릿의 상속은 상속받을 html파일의 최상단에 다음과 같이 적어줌으로써 이루어진다.

```
{% extends <base템플릿 경로> %}
``` 

#### form태그 시 주의사항

form태그 뒤에는 항상 `{% csrf token %}` 템플릿 태그를 넣어주어야 한다.

---

## MVC와 URL

여기서는 모델, 뷰, 템플릿, URL의 관계에 대해서 알아본다.

### MVC pattern과 Request&Response

#### MVC pattern

Model-View-Controller pattern 

> Django: Model-Template-View, MTV모델

- Model: Data (DB)
- View: 사용자에게 제공되는 화면(또는 기능)
	- Django의 Template (HTML)
	
- Controller: Model과 View사이에서 데이터를 가공하는 역할 <- urlresolver에 연결
	- Django의 View (Python function)

#### Request와 Response간에 일어나는 일

1. 사용자의 요청이 server에 도달 (URL로의 HTTP요청)
2. server는 해당 요청 URL을 Django에 전달
3. Django는 전달받은 URL을 urlresolver로 분석해서 작업을 처리할 Controller(View)에 연결
4. Controller는 요청을 받아 사용자에게 제공할 View(Template)를 응답으로 리턴
5. server는 리턴받은 응답을 사용자에게 전달


### URL매칭과 {% url %} 태그의 사용

장고는 도메인 뒤의 URL에만 관여한다.

#### URL

```
매칭패턴: r'^post/detail/(?P<pk>\d+)/'
컨트롤러: def post_detail()
URL의 이름: post_detail
```

1. 요청이 왔을경우
	- URL이 매칭되는 패턴을 찾는다
	- 해당 패턴에 할당된 컨트롤러가 작업을 처리

2. 특정 컨트롤러의 요청을 받을 수 있는 URL을 생성하고자 할 경우  
   URL이름을 고정해서 사용
   
	특정 컨트롤러는 이름이 바뀔 수 있음 (또는 다른 컨트롤러가 배정될 수 있음)  
	URL이름을 기준으로, 매칭패턴을 역(reverse)으로 사용해서 문자열을 생성  
	ex) `post_detail`이라는 이름의 URL에서, pk는 3에 해당하는 URL을 만들려면  
	-> `{% url 'post_detail' pk=3 %}`태그에 의해서 생성됨  
	-> `post/detail/3/`
	
---

### 스태틱 파일

#### 스태틱 폴더 생성

갖가지 정적 파일이나, css파일을 사용하기 위해 STATIC 폴더를 생성하여 준다. 템플릿 폴더와 같은레벨 즉 장고 애플리케이션 폴더 하위에 `static` 이라는 이름으로 생성하여 준다. css파일을 위한 `css` 폴더, image파일을 위한 `image`폴더, bootstrap을 위한 `bootstrap`폴더 등을 `static`폴더 하위에 필요에 따라 각각 만들어준다.

이후에는 템플릿과 마찬가지로 `STATIC_DIR`을 설정하여 주고, `STATICFILES_DIRS` 라는 변수를 만들어 `STATIC_DIR`을 리스트 형태로 넣어준다. 이렇게 함으로써 템플릿과 마찬가지로 파일 입출력을 통해 매번 스태틱파일 경로 위치를 찾는 수고를 덜 수 있다.

#### 스태틱 폴더의 사용

생성되어진 스태틱 폴더를 이용해 스태틱 파일의 경로를 html파일에서 손쉽게 불러들일 수 있다.

스태틱 파일을 사용할 html파일 상단 부분에 `{% load static %}` 이라고 써준 후 스태틱 파일을 사용할 태그의 `href` 부분에 `{% static <static파일 하위 경로> %}` 를 적어주면 된다.

#### bootstrap

http://bootstrapk.com/