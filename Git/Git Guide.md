# Git Guide

## 개요

상황별 git의 기본 사용법을 정리하여 기록한다.

## GitHub Repository 생성 & 소스 올리기

GitHub 사이트에 접속하여 Repository를 만들고, 로컬에 있는 파일을 Commit해 본다.

### Git Repository 생성

[github 가기](https://github.com/)

1. Github 사이트 로그인
2. 오른쪽 "+" 아이콘 클릭
3. New repository 클릭
4. Repository name dlqfur
5. Create Repository 버튼 클릭

### git init

이 명령은 `.git`이라는 하위 디렉터리를 만든다. `.git` 디렉터리에는 저장소에 필요한 Skeleton 파일이 있다.

```bash
$git init
```

1. 자신의 프로젝트 폴더에서 오른쪽 마우스 버튼 클릭
2. Git Bash Here 선택
3. `git init` 명령 실행

### git status

이 명령은 파일의 상태를 보여준다. 파일상태가 Tracked이면 변경이 없는 것을 뜻한다. 파일상태가 Untracked 상태라는 것은 로컬 레포지토리에 등록되지 않은 상태로 본다.

```shell
$git status
```

1. `git status`명령 실행
2. Untracked 상태 파일  없는지 확인

### git add

`git add`명령은 파일을 새로 추적관리 할 수 있게해준다.  

```shell
$git add <file name or folder name>
```

1. `git add <file name>`명령 실행
2. `git status` 명령으로 추가한 파일이 Staged상태이며 Tracked 상태인지 확인

### git commit

`git commit` 명령으로 Statged 상태에 있는 파일을 로컬 저장소에 기록한다.

```shell
$git commit -m "commit comment"
```

1. `git commit` 명령 실행

### git remote

작업 디렉터리에 리모트 저장소 정보를 추가한다.

```shell
$git remote add <단축이름> <URL>
```

1. GitHub에서 Remote 저장소 URL 복사
2. `git remote` 명령 실행
3. `git remote -v`명령을 실행하여 확인 Remote 저장소 확인

### git push

Staged 상태의 파일을 리모트 저장소에 등록한다.

```shell
$git push <remote repository name> <branch name>
```

1. `git push`명령 실행
2. GitHub에 정상적으로 Upload되었는지 확인