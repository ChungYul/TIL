# Gitignore

## 개요

SVN과 Eclipse 환경에서 개발할 때, Checkout 한 Project가 빌드되지 않았던 경험이 꽤 있었다. 환경 값을 저장하는 파일들이 함께 Checkout 되어 빌드에 영향을 미쳤기 때문인데. git에서는 명시적으로 untracked 상태로 두어야 할 파일의 패턴을 정의할 수 있다. 이를 gitignore 라 한다.

## gitignore 만들고 적용하기

gitignore를 적용 방법과 패턴을 정리한다.

자동으로 `.gitignore`를 만들어 주는 사이트를 소개한다.

### 적용방법

gitignore를 적용하는 방법은 3가지가 존재하고, 각 경우는 명확한 의도가 있다.

1. `.gitignore` : Version-Controlled 되어야 하고, 다른 Repository에 `clone` 으로 배포되어야 하는 패턴
2. `$GIT_DIR/info/exclude` : 특정 Repository에는 필요하지만 공유 할 필요없는 패턴
3. `core.excludeFile` : 모든 상황에서 무시되어야 하는 패턴

### 적용순서

1. Patterns read from the command line for those commands that support them.
2. Patterns read from a `.gitignore` file
3. Patterns read from `$GIT_DIR/info/exclude`
4. Patterns read from the file specified by the configuration variable `core.excludeFile`

### Pattern Format

필수 Pattern Format 아래와 같고 더 많은 정보는 [가이드]( https://git-scm.com/docs/gitignore) 를 참고한다. 

- 공백(Blank Line)은 Sperator 역할을 한다.
- `#` 로 시작되는 줄(Line)은 주석 처리된다.
- 후행 공백은 백 슬래시(" `\` ")를 이용하지 않으면 무시된다.
- Prefix " `!` " 는 전에 나왔던 패턴을 부정한다. 다시 파일과 디렉터리를 포함시킨다.
- " `*` " 는 " `/` " 를 제외한 모든 것을 매치 시킨다.
- " `?` " 는 " `/` " 를 제외한 한 글자를 매치 시킨다.

### 자동으로 파일 만들기

[gitignore](https://www.gitignore.io/) 에서 `.gitignore` 파일을 만들 수 있다.

### Notes

gitignore 파일의 목적은 남아있는 untracked 된 파일을 무시하기 위한 것이다.

이미 Tracked 되고 있는 파일 Tracking 을 중지 시키려면, `git rm --cached`  를 사용한다.

## 참고

1. https://git-scm.com/docs/gitignore
2. https://www.gitignore.io/
3. https://nesoy.github.io/articles/2017-01/Git-Ignore