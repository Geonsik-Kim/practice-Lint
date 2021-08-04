# practice-Lint
Lint 기본 학습을 위한 저장소<br>
'참고'에 있는 영상과 블로그를 따라서 진행하였습니다.

## 참고
프론트엔드 개발환경 이해 6강 - 린트(Lint) 기본 - 김정환<br>
[영상](https://youtu.be/BC-VrPsjkso)
[블로그](https://jeonghwan-kim.github.io/series/2019/12/30/frontend-dev-env-lint.html)
<br><br>
## 1. Lint
코드의 오류나 버그, 스타일 등을 점검하는 것을 Lint 혹은 Linter라고 부른다.<br>
Lint는 코드의 가독성을 높이는 것 뿐 아니라 런타임 버그를 예방할 수 있다.

<br><br>

## 2. ESLint
ESLint는 ECMAScript 코드에서 문제점을 검사하고 더 나은 코드로 정정 해주는 Lint 도구 중 하나이다.<br>
코드의 가독성을 높이고 잠재적인 오류와 버그를 제거하여 단단한 코드를 만드는 것이 목적이다.<br><br>

코드에서 검사하는 항목은 크게 2가지 이다.
* 포맷팅
* 코드 품질
<br><br>
<strong>포맷팅</storng> 일관된 코드 스타일을 유지하게 해준다. 예를 들어 "들여쓰기 규칙", "코드 라인의 최대 너비 규칙"등이 있다.<br>
<strong>코드품질</storng>은 잠재적인 오류나 버그를 예방하기 위함이다.

### 2.1 설치 및 사용법
설치
```
npm i -D eslint
```
환경설정 파일 생성
```
// .eslintrc.js
module.exports = {}
```
검사 대상 파일
```
app.js:
console.log();; // 세미콜론을 두개 사용
```
빈 객체로 아무런 설정없이 모듈만 만든상태이다. 이 상태에서 ESLint로 코드를 검사하면
```
npx eslint app.js
```
아무런 결과를 출력하지 않고 프로그램을 종료한다.

### 2.2 규칙(Rules)
ESLint는 검사 규칙을 미리 정해 놓았다. 문서의 [Rules](https://eslint.org/docs/rules/) 메뉴에서 규칙 목록을 확인할 수 있다.<br><br>
app.js에서 세미콜론은 두개 연속하여 사용한것과 관련된 규칙은 no-extra-semi 규칙이다.<br>
설정에 no-extra-semi 규칙을 추가하고,
```
// .eslintrc.js
module.exports = {
  rules: {
    "no-extra-semi": "error",
  },
}
```
코드를 검사하면 오류를 출력한다.
```
npx eslint app.js
1:15  error  Unnecessary semicolon  no-extra-semi

✖ 1 problem (1 error, 0 warnings)
  1 error and 0 warnings potentially fixable with the `--fix` option.
```
마지막 줄의 메세지를 보면 이 에러는 "잠재적으로 수정가능(potentially fixable)"하다고 말한다. --fix 옵션을 붙여 검사해보면,
```
npx eslint app.js --fix
```
검사 후 오류가 발생하면 자동으로 수정한다.<br>
이렇게 ESLint에서는 자동 수정이 가능한 것과 아닌것이있다<br>[규칙목록](https://eslint.org/docs/rules/) 중dp 왼쪽에 체크 표시되어 있는것이 "--fix" 옵션으로 자동 수정할 수 있는 규칙이다.
<br><br>

### 2.3 Extensible Config
이러한 규칙을 여러게 미리 정해 놓은 것이 eslint:recommended 설정이다.<br>[규칙목록](https://eslint.org/docs/rules/) 중에 왼쪽에 체크 표시되어 있는것이 이 설정에서 활성화되어 있는 규칙이다.
```
// .eslintrc.js
module.exports = {
  extends: [
    "eslint:recommended", // 미리 설정된 규칙 세트을 사용한다
  ],
}
```
만약 이 설정 외에 규칙이 더 필요하다면 rules 속성에 추가해서 확장할 수 있다.<br>
ESLint에서 기본으로 제공하는 설정 외에 자주 사용하는 두 가지가 있다.
* airbnb
* standard
<br><br>
<strong>airbnb</strong> 설정은 airbnb 스타일 가이드를 따르는 규칙 모음이다.<br> [eslint-config-airbnb-base](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb-base) 패키지로 제공된다.
<br>
<strong>standard</strong> 설정은 자바스크립트 스탠다드 스타일을 사용한다.<br> [eslint-config-standard](https://github.com/standard/eslint-config-standard) 패키지로 제공된다.

<br><br>

### 2.4 초기화
사실 이러한 설정은 --init 옵션을 추가하면 손쉽게 구성할 수 있다.
```
npx eslint --init

? How would you like to use ESLint?
? What type of modules does your project use?
? Which framework does your project use?
? Where does your code run?
? How would you like to define a style for your project?
? Which style guide do you want to follow?
? What format do you want your config file to be in?
```
대화식 명령어로 진행되는데 모듈 시스템을 사용하는지, 어떤 프레임웍을 사용하는지, 어플리케이션이 어떤 환경에서 동작하는지 등에 답하면 된다. 답변에 따라 .eslintrc 파일을 자동으로 만들 수 있다.