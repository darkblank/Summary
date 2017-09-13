# git

---

## git?

분산 버전 관리 시스템 (DVCS) <br><br>
로컬 버전 관리 > 중앙 집중식 버전 관리 > 분산 버전 관리 <br><br>

### git doc

https://git-scm.com/book/ko/v2/ 에서 git에 관한 전체 내용 확인 가능하다.

---

### git 설치

git 설치는 [이 곳](https://github.com/darkblank/Tips/blob/master/03_git.md)을 참조.

---

### 최초 설정

#### 사용자 정보

Git을 설치하고 나서 가장 먼저 해야 하는 것은 사용자이름과 이메일 주소를 설정하는 것이다. Git은 커밋할 때마다 이 정보를 사용한다. 한 번 커밋한 후에는 정보를 변경할 수 없다.

```
$ git config --global user.name <사용자 이름 ex)darkblank>
$ git config --global user.email <사용자 이메일 ex)darkblank1990@gmail.com)
```

#### 편집기

사용자 정보를 설정하고 나면 Git에서 사용할 텍스트 편집기를 고른다. 기본적으로 Git은 시스템의 기본 편집기를 사용한다. 다른 편집기를 사용하고 싶다면 다음처럼 설정하여준다.

```
$ git config --global core.editor <편집기 이름 ex)emacs>
```

#### 설정확인

`git config -list`명령을 실행하면 설정한 모든 것을 보여준다. 그래서 바로 확인할 수 있다.<br><br>

`git config <key>` 명령으로 Git이 특정 key에 대해 어떤 값을 사용하는지 확인할 수 있다.

```
$ git config user.name
darkblank
```
