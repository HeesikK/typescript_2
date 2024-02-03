# 📑 TypeScript Compile

## 🔎 tsc란?

`tsc`란 타입 스크립트 컴파일러 명령어이다. 일반적으로 컴파일(Compile)이란 소스 코드를 특정 플랫폼에서 실행 가능한 형태로
변환하는 과정을 의미한다. 타입 스크립트로 작성한 코드를 자바 스크립트 코드로 변환할때 필요한 것이 타입 스크립트 컴파일러이다.
타입스크립트 컴파일러는 코드 변환 과정에서 정적 타입 검사(static type check)를 해주기 때문에 프로그램 버그를 예방하는데
활용이 된다.

```javascript
// hello.ts

let name = "Levi";
console.log(name);
```

`tsc` 커맨드의 인자로 "hello.ts" 파일명을 넘기면 해당 파일에 저장되어 있던 소스 코드가 자바스크립트 파일로 변환된다.

```
$ npx tsc hello.ts
```

컴파일 결과 동일한 디렉토리에 파일 이름은 같지만 확장자가 .js인 파일이 추가되는 것을 확인할 수 있다

```javascript
// hello.js

let name = "Levi";
console.log(name);
```

## 🔎 tsconfig.json란?

`tsconfig.json`은 타입 스크립트를 위한 프로젝트 단위의 환경 파일로써 컴파일 옵션 및 컴파일 대상에 대한 설정을 기술한 것이다.
`tsconfig.json`을 작성하지 않으면 컴파일을 할때마다 다양한 옵션을 반복적으로 지정해줘야 하므로 `tsconfig.json`을 작성해 번거로운
작업을 피할 수 있다.

`tsc` 커맨드를 사용하면 타입 스크립트 컴파일러는 현재 디렉토리에서 `tsconfig.json` 파일을 찾고 해당 파일에 설정된 대로 컴파일을 수행한다. </br> 간단히 말해서 `tsconfig.json`은 타입 스크립트 프로젝트의 설정을 담당하고, `tsc`는 `tsconfig.json` 설정을 기반으로 타입 스크립트 코드를 컴파일 하는 명령어이다.

## 🔎 tsconfig.json을 사용해보자

### tsconfig.json의 주요 프로퍼티 - compilerOptions

`compilerOptions`을 사용해 컴파일 옵션을 설정한다. 생략한 경우 기본 컴파일 옵션이 사용된다.

```javascript
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "sourceMap": true,
    "strict": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "strictPropertyInitialization": true,
    "alwaysStrict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "allowJs": true,
    "checkJs": true,
    "jsx": "preserve",
    "declaration": true,
    "outFile": "app.js",
    "outDir": "./dist",
    "rootDir": "./",
    "removeComments": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "baseUrl": "./src",
    "paths": {
      "@myUtils/*": ["utils/*"]
    }
  }
}
```

- `target` 를 사용하여 tsc 커맨드로 최종 컴파일하는 결과의 문법 형태를 결정할 수 있다. 만약 위와 같이 `"target": "es5"`를 선택했다면 코드상에서 작성한 `() => {}`와 같은 화살표 함수는 모두 function 표현볍으로 변환된다. `target`에 따라서 사용할 수 있는 기능이 제한적이다.
- `module` 은 자바 스크립트 파일간 import 문법을 구현할때 어떤 문법을 사용할지 정하는 것이다. commonjs는 require 문법, es2015 및 esnext는 import 문법을 사용한다.
- `sourceMap` 을 true로 지정하면 결과물에 `.js.map` 이나 `.jsx.map` 파일이 포함된다.
- `strict` 를 true로 지정하면 타입 스크립트의 type 검사 옵션 중 `strict*` 와 관련된 모든 것을 true로 만든다. 즉 `strict*` 와 관련된 모든 속성(`strictNullChecks`, `strictFunctionTypes`)이 true 이므로 필요에 따라서 속성을 선택하여 false로 지정해야 한다.
- `strictNullChecks` 는 `null` 또는 `undefined` 여부를 엄격하게 검사하는데 사용되는 옵션이다.
- `strictFunctionTypes` 는 함수 매개변수의 타입을 검사하는데 사용하는 옵션이다.
- `strictPropertyInitialization` 는 클래스 생성자 작성시 타입을 검사하는데 사용하는 옵션이다.
- `alwaysStrict` 가 true로 설정되면 자바 스크립트 코드가 항상 `strict` 모드에서 실행된다.
- `noImplicitAny` 는 any 타입이 의도치않게 발생한 경우 에러를 띄워주는 설정이다.
- `allowJs` 를 true로 설정하면 `.js` 및 `.jsx` 파일도 컴파일 대상이 된다.
- `checkJs` 는 `.js` 파일도 타입 검사의 대상으로 삼을지 여부를 설정하는 옵션이다.
- `jsx` 는 어떻게 `.tsx` 파일을 `.jsx` 파일로 컴파일 할지 정하는 설정이다.(`preserve`, `react-native`, `react`)
- `declaration` 는 컴파일시 `.d.ts` 파일도 자동으로 함께 생성해주는 속성이다. `.d.ts` 파일은 현재쓰는 모든 타입이 정의된 파일이고 이 선언 파일은 주로 라이브러리나 모듈을 정의하고 다른 타입 스크립트의 프로젝트에서 사용할 때 타입 정보를 제공하는데 사용된다.
- `outFile` 을 사용하면 모든 `.ts` 파일을 하나의 `.js` 파일로 컴파일 해주는 설정이다.
- `outDir` 은 타입 스크립트 컴파일러에 의해 컴파일된 자바 스크립트 파일을 저장할 디렉토리를 지정하는데 사용된다.
- `rootDir` 은 루트 경로를 바꾸는 설정이다.
- `removeComments` 는 컴파일시 주석을 제거 하는 설정이다.
- `noUnusedLocals` 가 true이면 사용하지 않는 지역변수가 있을 경우 에러를 발생시킨다.
- `noUnusedParameters` 가 true이면 사용하지 않는 파라미터가 있을 경우 에러를 발생시킨다.
- `noImplicitReturns` 가 true이면 함수에서 return이 없다면 에러를 발생시킨다.
- `noFallthroughCasesInSwitch` 가 true이면 switch case 문에 문제가 있다면 에러를 발생시킨다.
- `baseUrl` 은 외부 모듈이 아닌 모듈들을 절대 경로로 참조할 수 있게 해준다. 만약 `"baseUrl": "./src"`로 설정하게 되면 src를 기준으로 절대 경로로 모듈 참조가 가능해진다.
- `baseUrl` 을 사용하여 절대 경로로 모듈을 참조할 수 있지만 `paths` 를 사용하면 별칭을 통해 더 상세하게 모듈을 참조할 수 있다.

### tsconfig.json의 주요 프로퍼티 - files

컴파일 대상을 지정하려면 `files` 또는 `include` 속성을 사용하면 된다. 만약 `files` 속성을 정의하였다면 `include` 속성은 무시된다.
`files` 속성에는 컴파일 대상 파일의 절대 경로 또는 상대 경로를 명시적으로 설정한다.

```javascript
{
  "files": [
    "src/example1.ts",
    "src/example2.ts"
  ]
}
```

### tsconfig.json의 주요 프로퍼티 - include, exclude

`include` 속성에는 컴파일 대상 파일 리스트를 설정한다. `exclude` 속성에는 컴파일 대상에서 제외할 파일 리스트를 설정한다.

- `*` 없거나 하나 이상의 문자열과 일치 (디렉토리 구분자 제외)
- `?` 하나의 문자와 일치 (디렉터리 구분자 제외)
- `**/` 단계에 관계없이 아무 디렉토리와 일치

```javascript
{
  "include":[
    "src/**/*"
  ],
  "exclude":[
    "node_modules",
    "**/*.example3.ts"
  ]
}
```
