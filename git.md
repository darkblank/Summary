# Git

---

## Git?

분산 버전 관리 시스템 (DVCS) <br><br>
로컬 버전 관리 > 중앙 집중식 버전 관리 > 분산 버전 관리 <br><br>

### Git doc

https://git-scm.com/book/ko/v2/ 에서 git에 관한 전체 내용 확인 가능하다.

---

### Git 설치

Git 설치는 [이 곳](https://github.com/darkblank/Tips/blob/master/03_git.md)을 참조.

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

`$git config -list`명령을 실행하면 설정한 모든 것을 보여준다. 그래서 바로 확인할 수 있다.<br><br>

`$git config <key>` 명령으로 Git이 특정 key에 대해 어떤 값을 사용하는지 확인할 수 있다.

```
$ git config user.name
darkblank
```
---

### 도움말 보기

`$git` 또는 `$git help`명령으로 자주 사용하는 명령들을 볼 수 있다.<br><br>

`$git help <명령>` 또는 `$git help <개념>` 명령으로 특정 하위 명령어나 개념에 대한 도움말을 볼 수 있다.

---

## Git 기초

### Git 저장소 만들기

기존 프로젝트나 디렉토리를 Git 저장소로 만드는 방법이 있고, 다른 서버에 있는 저장소를 Clone하는 방법이 있다.

#### 기존 디렉터리를 Git 저장소로 만들기

git으로 관리하고 싶은 프로젝트나 폴더로 이동한 다음 `$git init`명령을 이용하여 git 저장소를 만들어준다. 하지만 이 명령만으로는 프로젝트나 폴더 내부의 어떠한 파일도 관리하지 않는다. `$git add <파일명>`명령으로 저장소에 파일을 추가 한 후 `$git commit`명령을 통해 커밋을 해주면서 파일 버전 관리를 시작하게 된다.

#### 다른 서버에 있는 저장소를 Clone하기

`$git clone <url>`명령으로 저장소를 Clone 한다. 이 명령은 현재 위치한 디렉토리에 새 디렉토리를 만들고 그 안에 `.git`디렉토리를 만든다. 그리고 자동으로 데이터를 모두 가져와서 자동으로 가장 최신 버전을 Checkout 해 놓는다. 생성되어진 디렉토리로 이동하면 Checkout으로 생성한 파일을 볼 수 있고 당장 하고자 하는 일을 시작할 수 있다. 새 디렉토리의 이름을 직접 정하고 싶다면 다음과 같은 명령을 쓰면 된다.

```
$ git clone <url> <디렉토리명>
```

#### 파일 무시하기

어떤 파일은 Git이 관리할 필요가 없다. 보통 로그 파일이나 빌드 시스템이 자동으로 생성한 파일이 그렇다. 그런 파일을 무시하려면 `.gitignore` 파일을 만들고 그 안에 무시할 파일 패턴을 적는다. <br><br>

pyenv로 관리되어지는 폴더가 있다고 할 때, Git이 관리 할 필요가 없는 파일들이 무엇인지 알고 싶다면 https://www.gitignore.io/ 에서 어떤 파일들을 무시해야 할지 검색하여 볼 수 있다.<br><br>

`.gitignore` 파일에 입력하는 패턴은 아래 규칙을 따른다.

- 아무것도 없는 라인이나, `#`로 시작하는 라인은 무시한다.
- 표준 Glob 패턴을 사용한다.
- 슬래시(/)로 시작하면 하위 디렉토리에 적용되지(Recursivity) 않는다.
- 디렉토리는 슬래시(/)를 끝에 사용하는 것으로 표현한다.
- 느낌표(!)로 시작하는 패턴의 파일은 무시하지 않는다.<br><br>

`.gitignore` 파일의 예
```
# 확장자가 .a인 파일 무시
*.a

# 윗 라인에서 확장자가 .a인 파일은 무시하게 했지만 lib.a는 무시하지 않음
!lib.a

# 현재 디렉토리에 있는 TODO파일은 무시하고 subdir/TODO처럼 하위디렉토리에 있는 파일은 무시하지 않음
/TODO

# build/ 디렉토리에 있는 모든 파일은 무시
build/

# doc/notes.txt 파일은 무시하고 doc/server/arch.txt 파일은 무시하지 않음
doc/*.txt

# doc 디렉토리 아래의 모든 .pdf 파일을 무시
doc/**/*.pdf
```

---

### 파일의 상태 확인하기

파일의 상태를 확인하려면 보통 `$git status`명령을 사용한다. `$git status`명령은 폴더 내의 파일이 어떤 상태인지를 나타내주며 `add` 하여야 할 또는 `commit`하여야 할 파일들을 나타내 준다.<br><br>

또한 `git diff`라는 명령으로 확인할 수도 있는데, 이건 아직 쓸 일이 없었을 뿐더러 아직 자세히 어떠한 상황에 쓰는 것인지도 잘 몰라서 나중에 다시 적겠다.

---

### 파일 삭제, 이름 변경

#### 파일 삭제

`$git rm`명령으로 파일을 지우거나 했을 경우에도 커밋을 해주어야 한다. `$git rm`명령으로 파일을 지웠을 경우에는 실제로 워킹 디렉토리에 있는 파일도 없어지지만, `--cached`옵션을 사용하면 Staging Area에서만 제거되어지고 워킹 디렉토리에 있는 파일은 지우지 않고 남겨둘 수 있다. 

#### 파일 이름 변경

파일 이름이 바뀌었을 경우 또한 커밋을 해주어야 한다. `$git mv file_from file_to` 명령으로 이름을 바꿀 수 있다. 

  - 참고 : 파일 이름 변경을 한 상태로 수정을 한 후 Staging Area로 옮기는 과정에서 파일 내용 중 많은 부분이 수정되어진 경우 Git에서 바뀌어진 이름을 인지하지 못할 수 있다. (내용이 너무 바뀌었기 때문에) 이러한 경우에는 `$git diff -M`으로 이를 잡아줄 수 있다. 

---

### 커밋 히스토리 조회하기

`$git log`명령을 통하여 커밋 히스토리를 시간순으로 조회할 수 있다. 단, 현재의 헤드가 있는곳을 기준으로 그 이후의 커밋 히스토리는 보여주지 않는다. 이러한 경우에 모든 커밋 히스토리를 보고 싶다면 `--all` 옵션을 붙여주면 볼 수 있다. 또한 커밋 히스토리를 보고 싶다면 `--oneline`옵션을, `--graph`옵션으로 브랜치와 머지 히스토리를 보여주는 아스키 그래프를 출력할 수도 있다.

---

### 되돌리기

#### 커밋 수정하기

만약 어떠한 수정사항을 빠트리고 커밋을 진행하였다면 `--amend`옵션을 사용할 수 있다.

```
$ git commit --amend
```

이 명령은 Staging Area를 사용하여 커밋한다. 만약 마지막으로 커밋하고 나서 수정한 것이 없다면(커밋하자마자 바로 이 명령을 실행하는 경우) 조금 전에 한 커밋과 모든 것이 같다. 이때는 커밋 메시지만 수정한다. <br>
편집기가 실행되면 이전 커밋 메시지가 자동으로 포함된다. 메시지를 수정하지 않고 그대로 커밋해도 기존의 커밋을 덮어쓴다.<br>
커밋을 했는데 Stage 하는 것을 깜빡하고 빠트린 파일이 있으면 아래와 같이 고칠 수 있다. 

```
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

여기서 실행한 명령어 3개는 모두 커밋 한 개로 기록된다. 두 번째 커밋은 첫 번째 커밋을 덮어쓴다.

#### 파일 상태를 Unstage로 변경하기

실수로 `$git add -A` 명령을 이용해 원치 않는 파일까지 Staging Area로 넣었다면 다음 명령을 사용하여 Unstaged 상태로 변경할 수 있다.

```
$git reset HEAD <파일명>
```

`$git reset` 명령은 위험하기 때문에 조심해서 다룰 수 있도록 한다.

#### 최근 커밋 버전으로 되돌리기

수정한 파일을 최근 커밋한 상태로 되돌리고 싶다면 다음과 같은 명령을 사용할 수 있다.

```
$git checkout -- <파일명>
```

이 명령 또한 원래 파일로 덮어 씌우는 것이기 때문에 수정한 내용이 전부 사라지므로 상당히 위험한 명령이다. 수정한 내용이 정말 마음에 들지 않을 때에만 사용하도록 한다.

#### Branch와 Stash를 사용하여 되돌리기

Branch를 이용하면 수정한 내용을 버리지 않으면서 이전 시점으로 되돌릴 수 있다. 이전에 커밋한 부분으로 이동하여 새 Branch를 만들어주면 Branch를 오가면서 이전 시점으로 되돌릴 수도 있고, 수정 후 시점으로 되돌아올 수도 있다. <br><br>

또한 Stash 기능을 이용하여 쉽게 되돌릴 수도 있는데 `$git stash`명령을 쓰면 마지막 커밋으로부터 이 명령을 쓰는 시점까지의 변경사항을 Stash에 담아준다. 수정한 후 커밋을 하지 않은 상태라면 이 내용들을 Stash에 담아 놓을 수 있다. Stash에 담은 내용은 `$git stash pop`으로 불러들일 수 있고 `$git stash -u`명령으로 Untraked 파일까지 관리할 수 있다. **Stash를 이용하면 실수로 다른 브랜치에서 작업한 경우에도 손쉽게 처리할 수 있다.**

---

### 리모트 저장소

리모트 저장소는 인터넷이나 네트워크 어딘가에 있는 저장소로 다른 사람들과 일을 하기 위해서 리모트 저장소를 관리할 줄 알아야 한다.

#### 리모트 저장소 추가하기

다음과 같은 명령으로 리모트 저장소를 추가할 수 있다.

```
$git remote add <단축이름> <저장소url>
```

만약 단축이름에 아무것도 적지 않으면 단축이름은 자동으로 origin으로 생성되어진다.(아마도)

#### 리모트 저장소 확인하기

`$git remote` 명령으로 리모트 저장소의 단축 이름을 확인 할 수 있고<br>
`$git remote -v`로 리모트 저장소의 단축 이름과 url을 함께 확인할 수 있다.<br>
`$git remote show <리모트 저장소 단축이름>` 명령으로 리모트 저장소의 구체적인 정보를 확인할 수도 있다. 

#### 리모트 저장소의 데이터 가져오기(fetch, pull)

다음 명령으로 리모트 저장소에서 데이터를 가져올 수 있다.

```
$git fetch <리모트 저장소 단축이름>
```

이 명령으로 로컬에는 없지만 리모트 저장소에는 있는 데이터를 모두 가져온다. `fetch`명령은 리모트 저장소의 데이터를 모두 가져오지만 자동으로 `merge`시켜주지는 않는다. 따라서 로컬에서 하던 작업을 정리하고 수동으로 `merge`시켜주어야 한다.<br><br>

`$git pull` 명령을 사용하면 리모트 저장소 브랜치에서 데이터를 가져올 뿐 아니라 자동으로 로컬 브랜치와 `merge`시킬 수 있다. (아직 실제로 사용해 본 적이 없기 때문에 나중에 더 자세히 정리)

#### 리모트 저장소에 데이터 저장하기(push)

```
$git push <리모트 저장소 단축이름> <브랜치 이름>
```

위와 같은 명령으로 로컬 저장소의 내용을 리모트 저장소에 저장할 수 있다. 단, 이 명령은 다른 사람이 리모트 저장소의 내용을 수정하여 놓았다면 그 내용을 가져와서 `merge`한 후에 `push`하여야 한다.

#### 리모트 저장소 이름변경/삭제 하기

아래와 같은 명령으로 리모트 저장소의 이름이 변경 가능하다.

```
$git remote rename <원래이름> <바꿀이름>
```

아래와 같은 명령으로 리모트 저장소의 삭제가 가능하다.

```
$git remote remove <저장소 이름>
```

## 브랜치

### 브랜치란?

커밋 사이를 가볍게 이동할 수 있는 포인터 같은 것으로, 커밋을 할 때 마다 브랜치는 가장 마지막 커밋을 가리키게 된다.

#### 브랜치의 생성과 이동

아래와 같은 명령으로 브랜치를 생성할 수 있다.

```
$git branch <새 브랜치 이름>
```

브랜치를 생성한 후에는 다음과 같은 명령으로 다른 브랜치로 이동할 수 있다.
참고로 기본적으로 Git은 master 브랜치를 만들고 이 master 브랜치가 있는 커밋을 가르키고 있다.

```
$git checkout <브랜치 이름>
```

이렇게 새로운 브랜치를 생성한 후 해당 브랜치로 이동하여 커밋을 하게 되면 master 브랜치는 이전 커밋에 남아있게 되고 새로운 브랜치가 앞으로 이동하게 된다.<br><br>

다음과 같은 명령으로 브랜치를 생성하면서 그 브랜치로 이동할 수 있다.

```
$git checkout -b <새 브랜치 이름>
```

---

### merge의 기초

이 부분은 [이 링크](https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%99%80-Merge-%EC%9D%98-%EA%B8%B0%EC%B4%88)를 참조하여 그림과 함께 보는 것이 좋을 듯 하다.

---

### 브랜치 관리

`$git branch` 명령으로 현재 브랜치의 목록을 볼 수 있다. * 표시가 붙어있는 브랜치는 현재 checkout 해서 작업하는 브랜치를 나타낸다. 즉, 지금 수정한 내용을 커밋하게 되면 * 표시가 붙어있는 브랜치가 한 단계 앞으로 나아간다. `$git branch -v` 명령을 실행하면 브랜치마다 마지막 커밋 메시지도 볼 수 있다.<br><br>

각 브랜치의 현재 상태를 확인하기 좋은 옵션도 있다. 현재 checkout 한 브랜치를 기준으로 merge 된 브랜치인지 그렇지 않은지 필터링 해 볼 수 있다. 명령은 아래와 같다.

```
$git branch -merged
$git branch -no-merged
```

여기서 `-merged`옵션으로 확인한 브랜치 중 * 표시가 붙어있지 않은 브랜치는 이미 다른 브랜치와 merge 했기 때문에 삭제해도 정보를 잃지 않는다. 브랜치 삭제 명령은 다음과 같다

```
$git branch -d <브랜치 이름>
```

merge하지 않은 브랜치를 강제로 삭제하는 옵션은 `-d` 대신 `-D`를 쓰면 된다. 

---

### 리모트 브랜치

자세한 내용은 [이 링크](https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%A6%AC%EB%AA%A8%ED%8A%B8-%EB%B8%8C%EB%9E%9C%EC%B9%98)를 참조 하도록 하고, 리모트 저장소의 리모트 브랜치를 수업시간에 진행했던 간단한 협업 과정을 통해 알아본다.

#### 협업이 이루어지는 과정

'사용자 1'이 리모트 저장소를 만들고 협업을 하기로 한 '사용자 2'를 리모트 저장소로 초대한다.<br><br>

'사용자1'이 새 파일을 만들어서 커밋을 한 뒤 Push한다.<br><br>

'사용자2'가 이 리모트 저장소를 Clone을 하게 되면 Git은 자동으로 `origin`이라는 이름을 저장소에 붙이고 `orgin`으로부터 저장소 데이터를 모두 내려받은 후 `master` 브랜치를 가리키는 포인터를 만드는데, 이 포인터는 `origin/master`라고 부르고 멋대로 조종할 수 없다. 그리고 Git은 로컬의 `master` 브랜치가 `origin/master`를 가리키게 한다. <br><br>

'사용자1'이 브랜치를 새로 만들고 파일을 하나 만들어서 커밋 한 후 새로만든 브랜치를 통해 푸쉬를 한다. 이 새로만든 브랜치의 이름을 `dev`라고 하자.<br><br>

'사용자2'가 `fetch`를 통하여 '사용자1'이 Push한 내용을 받아오면 새로운 리모트 브랜치인 origin/dev가 생성되어 있다.<br><br>

'사용자2'는 새로 받아온 내용과 로컬 내용을 `merge`하기를 원한다면 `$git merge origin/dev` 명령을 사용할 수 있고, 우리는 `merge`하지 않고 리모트 트래킹 브랜치에서 시작하는 새 브랜치를 만들어 작업을 하기를 원하기 때문에 아래와 같은 명령을 사용하여 준다.

```
$git checkout -b dev origin/dev
```

이렇게 하면 `origin/dev` 로부터 시작하고 수정할 수 있는 `dev`라는 로컬 브랜치가 만들어진다.<br><br>

각자 새로 만든 `dev` 브랜치를 기준으로 브랜치를 하나씩 생성한다. 여기서 각자의 브랜치 이름은 `feature/list`와 `feature/form`이라고 하자.<br><br>

각자 서로 로컬 저장소에서 내부의 내용을 다르게 수정하고 각자 커밋을 진행한다.<br><br>

이후 '사용자1'이 `feature/list` 브랜치로 푸쉬를 진행하고 `pull request`로 `origin/dev`로 `merge`해도 되겠냐는 요청을 보내고 승인을 받게되면 리모트 저장소에서 `feature/list`가 `origin/dev`로 `merge`되어진다. 이후에 `feature/list`브랜치는 `merge`되어졌기 때문에 삭제해도 된다.<br><br>

바뀐 내용이 있는 리모트 저장소에서 '사용자 2'가 `fetch`를 이용해 받아온다. 받아온 내용을 자신의 로컬 저장소 내의 브랜치인 `feature/form`으로 `chekout`을 한 후 `origin/dev`를 merge 시킨다.<br><br>

같은 부분을 서로 다르게 수정한 내용이 있기 때문에 충돌이 일어나게 되고, 이 충돌이 일어난 부분을 fix해준 후 커밋하고 `feature/form` 브랜치로 푸쉬를 진행한다.<br><br>

푸쉬 한 후에 `pull request`로 `dev`로 `merge`해도 되겠냐는 요청 후에 승인을 받게되면 리모트 저장소에서 `feature/form` 브랜치를 `origin/dev`로 `merge`를 진행한다. 이후에 `feature/form` 브랜치는 `merge`되었기 때문에 삭제해도 무방하다.

---

### Rebase

쓸 일도 없고 잘 몰라서 추후 정리.
