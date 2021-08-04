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
<br><br>
## 3. Prettier
Prettier는 코드를 "더" 예쁘게 만들어준다.<br>
ESLint의 포매팅과 겹치는 부분이 있지만 Prettier는 좀 더 일관적인 스타일로 코드를 다듬어준다.<br>
반면 코드품질과 관련된 기능은 하지 않는 것이 ESLint와 다른 점이다.<br><br>
### 3.1 설치 및 사용법
설치
```
npm i -D prettier
```
검사 대상 파일
```
// app.js:
console.log("hello world")
```
검사
```
npx prettier app.js --write
```
"--write" 옵션을 추가하면 파일을 재작성한다. 그렇지 않을 경우 결과를 터미널에 출력한다.<br>
변경된 모습을 보면
```
// app.js
console.log("Hello world")
```
작은 따옴표를 큰 따옴표로 변경하고 문장 뒤에 세미콜론이 추가 되었다.<br>
ESLint와 달리 규칙이 미리 세팅 되어 있기 때문에 설정없이 바로 사용이 가능하다.

### 3.2 포매팅(더 예쁘게)
```
// app.js
console.log("----------------매 우 긴 문 장 입 니 다 80자가 넘 는 코 드 입 니 다.----------------")
```
위 같은 경우 ESLint는 [max-len](https://eslint.org/docs/rules/max-len) 규칙을 이용해 코드를 검사하고 결과를 알려줄 뿐 수정은 개발자의 몫이다.<br>
반면 Prettier는 어떻게 수정해야하는 지 알고 있기 때문에 아래처럼 코드를 다시 작성한다.
```
// app.js
console.log(
  "----------------매 우 긴 문 장 입 니 다 80자가 넘 는 코 드 입 니 다.----------------"
);
```

## 4. ESLint와 Prettier 통합하기
포맷팅은 간편한 Prettier에게 맡기더라도 코드품질과 관련된 검사는 ESLint의 몫이다.<br>
따라서 이 둘을 같이 사용한다면 최선의 방법일 것이다.<br>
Prettier는 이러한 ESLint와 통합 방법을 제공한다.<br>
[eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)는 Prettier와 충돌하는 ESLint 규칙을 끄는 역할을 한다. 둘다 사용하는 경우 규칙이 충돌하기 때문이다.
<br><br>
설치
```
npm i -D eslint-config-prettier
```
설정파일의 extends 배열에 추가한다.
```
// .eslintrc.js
{
  extends: [
    "eslint:recommended",
    "eslint-config-prettier"
  ]
}
```
예를 들어 ESLint는 중복 세미콜론 사용을 검사한다. 이것은 Prettier도 마찬가지다.<br>
따라서 어느 한쪽에서는 규칙을 꺼야하는데 eslint-config-prettier를 extends 하면 중복되는 ESLint 규칙을 비활성화 한다.
```
var foo = "" // 사용하지 않은 변수. ESLint가 검사
console.log();; // 중복 세미콜론 사용. 프리티어가 자동 수정
```
ESLint는 중복된 포매팅 규칙을 Prettier에게 맡기고 나머지 코드품질에 관한 검사만 한다.<br>
따라서 아래처럼 두 개를 동시에 실행해서 코드를 검사한다.
```
npx prettier app.js --write && npx eslint app.js --fix

1:5  error  'foo' is assigned a value but never used  no-unused-vars

✖ 1 problem (1 error, 0 warnings)
```
Prettier에 의해 코드가 아래와 같이 포매팅 되었고
```
var foo = ""
console.log();
```
ESlint에 의해 코드품질과 관련된 오류(no-unused-vars)를 리포팅한다.
<br><br>
한편, [eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier)는 Prettier 규칙을 ESLint 규칙으로 추가하는 플러그인이다. 프리티어의 모든 규칙이 ESLint로 들어오기 때문에 ESLint만 실행하면 된다.<br>
패키지를 설치하고
```
npm i -D eslint-plugin-prettier
```
설정 파일에서 pulugins와 rules에 설정을 추가한다.
```
// .eslintrc.js
{
  plugins: [
    "prettier"
  ],
  rules: {
    "prettier/prettier": "error"
  },
}
```
Prettier의 모든 규칙을 ESLint 규칙으로 가져온 설정이다.<br>
이제는 ESLint만 실행해도 Prettier의 포매팅 기능을 사용할 수 있다.
```
npx eslint app.js --fix
```
Prettier는 이 두 패키지를 함께 사용하는 단순한 설정을 제공한다.
```
// .eslintrc.js
{
  "extends": [
    "eslint:recommended",
    "plugin:prettier/recommended"
  ]
}
```