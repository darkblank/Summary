# Django

파이썬으로 만들어진 무료 오픈소스 웹 애플리케이션 프레임워크<br>
쉽고 빠르게 웹사이트를 개발할 수 있도록 돕는 구성요소로 이루어진 웹 프레임워크

## Django 시작을 위한 환경 구축

### 프로젝트 폴더 생성

Django project 이름으로 되어진 프로젝트 폴더를 생성하고 이 폴더를 git을 통해서 관리를 해준다.

`.gitignore`에는 **Django, Python, Linux, Pycharm** 가 포함되어야 한다. 추가로 Pycharm때문에 생기는 **.idea/** 라는 것도 포함 해준다.

pyenv로 가상환경을 적용하여 주고 프로젝트 폴더를 Github과 연결 시켜준다.

Pycharm으로 해당 프로젝트 폴더 open 후 interpreter설정을 해준다.

`$pip install`을 이용하여 가상환경에 **django, ipython, django_extensions** 를 설치하여 준다.

설치 후 requirements와 readme를 만들어준다.

---

### 애플리케이션 폴더 생성

`$django-admin startproject <프로젝트명>` 으로 애플리케이션 폴더를 생성한다. 그럼 `manage.py`를 가진 애플리케이션 폴더와, 애플리케이션 폴더와 이름이 같은 세팅폴더가 생긴다. 두 폴더의 이름이 같기 때문에 쉽게 구분할 수 있게 하기 위해 세팅폴더의 이름을 바꾸어 주는 것이 좋다.

파이참에서 source root는 애플리케이션 폴더로 지정한다.

#### 세팅폴더 폴더명 변경법

세팅폴더는 그냥 폴더가 아니라 하나의 패키지이다. 정확히는 애플리케이션 폴더까지만 폴더이고, 세팅폴더는 패키지이다. 세팅폴더의 폴더명을 바꾸려면 Pycharm에서 세팅폴더에 오른쪽 마우스를 눌러서 `refactor > rename`을 이용하여 dialog 박스 내의 모든 옵션에 체크를 하고 `refactor`를 실행한다. 그럼 어느 부분을 바꿀 것인지 보여주는데 다시 한번 확인을 하고 `do refactor`를 눌러서 바꾸어준다.<br>
폴더명은 config를 추천한다.

---

### 내부 애플리케이션 폴더 생성

`manage.py`가 있는 곳에서 `$python manage.py startapp <이름>` 으로 내부 애플리케이션 폴더를 생성하여 준다. 폴더와 각종 모듈이 같이 생성되어진다.

이후 이 패키지를 장고 내부에서 애플리케이션 단위로 인식하게 하기 위해서 `settings.py` 의 INSTALLED_APPS에 폴더명을 추가 해주어야 한다.

---

### sqlitebrowser 설치

SQLite와 호환되는 데이터베이스 파일을 생성, 디자인 및 편집 할 수 있는 고품질의 시각적 오픈 소스 도구

```
$sudo add-apt-repository -y ppa:linuxgndu/sqlitebrowser
$sudo apt-get update
sudo apt-get install sqlitebrowser
```

위의 명령을 통해 설치를 해준다.

공식 홈페이지 : http://sqlitebrowser.org/

---

### 프로젝트 구조

위에서 만든 프로젝트 구조는 다음과 같다

```
projects/
	django/ # Django project들
		프로젝트 폴더/ # Django project folder
			.git
			.gitignore
			  Django, Python, Linux, macOS,
			  PyCharm
			  # Custom
			  .idea/
			.python-version (pyenv local)
			requirements.txt

			애플리케이션 폴더/ # Django application folder
				manage.py
				세팅 폴더(패키지)/ # Django settings folder
					__init__.py
					settings.py
					urls.py
					wsgi.py
				내부 애플리케이션 폴더/ (ex.blog, mysite, etc.)
					migrations/
					__init__.py
					admin.py
					apps.py
					models.py
					tests.py
					views.py	
```

---

### secret_key 숨기기

`startproject`로 생성되어진 폴더와 같은 레벨에 `.config_secret`같은 숨겨진 폴더를 생성한다.

그 안쪽에 `settings_common.json`같은 `json`파일을 생성하여 준다.

아래 내용은 `json`파일 안에 들어갈 내용이다.

```json
{
  "django": {
    "secret_key": "aa_ho^$5910f-%bb6!h!th^p_koop5szllm&_1*rc)+df)$t)t",
    "databases": {
      "default": {
        "ENGINE": "django.db.backends.postgresql",
        "HOST": "localhost",
        "PORT": "5432",
        "NAME": "",
        "USER": "",
        "PASSWORD": ""
      }
    }
  }
}
```

이제 `setting.py`의 **SECRETKEY** 와 **DATABASES** 의 내용을 지워주고
위 파일의 내용으로 대체하여야 한다. 그러기 위해서는 `settings.py` 내부에 다음과 같은 작업을 해준다.

```python
ROOT_DIR = os.path.dirname(BASE_DIR)
CONFIG_SECRET_DIR = os.path.join(ROOT_DIR, '.config_secret')

with open(os.path.join(CONFIG_SECRET_DIR, 'settings_common.json'), 'rt') as f:
    config_secret_common_str = f.read()
config_secret_common = json.loads(config_secret_common_str)
```

위와 같이 작업 해줌으로써 `config_secret_common`이라는 변수에 우리가 `json`파일에 담은 딕셔너리 형태의 내용이 들어가게 된다. 따라서 **SECRETKEY** 와 **DATABASES** 변수에 위의 딕셔너리 형태의 내용을 다음과 같이 담아주도록 한다.

```python
SECRET_KEY = config_secret_common['django']['secret_key']
DATABASES = config_secret_common['django']['databases']
```

---

### 디버깅 설정법

우측 상단 또는 **Run** 메뉴의 **Edit Configurations** 설정으로 들어가서 왼쪽 상단의 `+`를 눌러주고 `Python`을 선택하여준다.

**Name** 부분에 적절한 이름을 설정하여준다.(Django runserver 추천) 

**Script** 부분에 `manage.py` 설정하여준다.

**Script parameters** 에 `runserver` 입력하여준다.

**Working directory** 에는 `소스루트로 지정한 폴더, 즉 장고 애플리케이션 폴더`를 지정하여 준다.

#### 디버깅시 runserver 오류가 날 때

아무리 찾아도 현재 돌아가고 있는 runserver가 없을 때 다음과 같은 명령어를 실행하여 돌아가고 있는 runserver를 찾아서 죽일 수 있다.

```
$ps -ax | grep runserver 
#현재 실행되어지는 프로세스중에 runserver 확인

$kill -9 <ID넘버> <ID넘버> 
#실행되어지는 프로세스 죽이기
```
