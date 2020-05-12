# Git 상태

## 개요

`git init` 명령을 실행하면, .git directory가 생긴다.

`git status` 명령을 실행하면, 파일 상태를 구분하여 보여준다.

무슨 일이 일어나는 걸까?

## Three Main States

git에서 관리하는 파일은 Modified, Staged, Commited 중 3가지 상태를 갖는다. `git status` 명령을 통해 확인 가능하다. 각 상태가 무슨 의미를 갖는지 확인한다.

### Git Project의 3가지 구분

- ##### .git directory(Repository)

​       Git 프로젝트의 메타 데이터와 객체 데이터베이스가 이 디렉터리에 저장된다.

​       `git clone`과 `git init`명령 등으로 .git diretory가 만들어 진다.

- ##### Working Directory

​       일반적으로 사용자가 작업하는 디렉터리이다. 

​        Working Directory의 파일은 .git directory에 압축된 데이터 베이스로부터 파일이 추출되어 디렉터리에 위치된다.

- ##### Staging Area

​       .git directory에 포함된 파일로 곧 커밋 할 파일 정보를 저장한다.

##### 기본적인 Git 의 작업 순서

1. Working Directory에 있는 파일을 수정한다.
2. 커밋 할 파일들을 Staging Area로 추가한다. (`git add` 명령어 사용)
3. Staging Area에 있는 파일들을 커밋하고, .git directory에 스냅샷을 저장한다. (`git commit` 명령어 사용)

### Working Directory 파일 구분

Working Directory의 파일은 tracked와 untracked로 구분된다.

- ##### tracked

​       이미 스냅샷에 관리되어 있던 파일이다. 즉, 변경되면 git에서 변경을 감지하는 파일이다.

- ##### untracked

​       .git directory에 해당 파일의 정보를 찾을 수 없는 파일로 일반적으로 `checkout` 이후 새로 생성된 파일이다.

### tracked 파일 상태

.git directory 에서 관리하는 파일은 Modified, Staged, Committed 3가지 상태로 구분하여 관리한다.

- ##### Modified

​       you have changed the file but have not committed it to your database yet.

- ##### Staged

​       you have marked a modified file in its current version to go into your next commit snapshot.

- ##### Committed

​       the data is safely stored in your local database.

## 참고

1. [Pro Git 2nd Edition](https://git-scm.com/book/ko/v2)