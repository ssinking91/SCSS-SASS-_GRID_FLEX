### 💫 SCSS-SASS-\_GRID_FLEX

<br />

---

<br />

### ✔️ Live Sass Compiler 설정

```javascript
vscode => setting.json

{
  // 컴파일 포맷 방식 작성
  "liveSassCompile.settings.formats": [
    // This is the default.
    {
      "format": "expanded",
      "extensionName": ".css",

      // null for all three -> denotes the same path as the SASS file
      // "savePath": null,
      "savePath": "/css",
      "savePathReplacementPairs": null
    }
  ],

  // map 파일 사용 유무(Default : true) - 소스맵 사용안할 경우 false로 설정
  "liveSassCompile.settings.generateMap": false,

  // 자동 밴더 프리픽스 사용하게 해줌.
  "liveSassCompile.settings.autoprefix": ["> 1%", "last 2 versions"]
  // "liveSassCompile.settings.autoprefix": null
}
```

- ⭐ 출력창 안보이기
  - Ctrl + , => sass => Live Sass Compiler => Show output Window on : None

<br />

---

<br />

### ✨ 1. SCSS 핵심 이론(Essential Theory)

(1) 선택자 중첩(Nesting)

- body는 독립적으로 => reset으로 사용

<br />

(2) 부모 선택자 참조(&)와 주석⭐

- &(Ampersand) = 부모요소 선택자
- 주석 = `/* */` or `//`
- `a` 태그는 inline 속성이기때문에 크기 값을 가질수 없음 => display : block / inline-block
- `:before :after` 태그는 inline 속성이기때문에 크기 값을 가질수 없음 => position : absolute가 되면 모든 요소는 inline-block으로 display 속성이 변함⭐

<br />

(3) 부모 선택자 참조 응용

- `class="font-large"` => `.font {&-large{ ... }}`

<br />

(4) 대표적인 CSS 선택자 SCSS에서 만들기

- 태그와 함께쓰는 선택자 : `p.center { ... }` => p와 .center 사이 띄어쓰기 하지 말것⭐
- 그룹선택자 : `h1,p span { ... }` => 콤마(,)로 연결, 연결 선택자라고도 함⭐
- 공통적으로 사용 할 UI는 부모요소 밖에서 CSS를 하여 재사용이 가능하도록 만들것

<br />

(5) 부모 선택자 참조, 가상클래스

- 가상클래스 `&:hover, &:nth-child(n), &:first-child, &:before, &:after, &::placeholder`등 &와 연결해서 사용
- 아이디, 클래스 속성선택자 `&#id-name, &.class-name, &[type="radio"]`등 &와 연결해서 사용
- `body {font-family:...}`는 input태그에 적용되지 않음 => `* {font-family:...}`로 변경⭐
- `button`태그는 `transition: 0.35s`가 가장 적당함⭐

<br />

(6) 부모 선택자 참조, 속성선택자

- `<input type="button">` => `선택자[속성="값"] {...}` === `input[type="button"] {...}`
- `<input type="button" value="텍스트 내용">`
- `input`, `button`태그는 display: inline-block 이 기본요소 => display: block을 하더라도 width: 100% 를 주어야 함⭐

<br />

(7) 부모선택자 중첩 나가기 @at-root

- `@ : 골뱅이(at sign)`
- `& : 앰퍼샌드(ampersand)`
- `~ : 물결(tild)`
- `^ : 눈꼬리(caret)`

<br />

(8) 접두어(prefix) 사용해서 CSS 속성 자동생성

```scss
font: {
  family: "Raleway", sans-serif;
  size: 18px;
  weight: 500;
}

text: {
  align: center;
  overflow: hidden;
  transform: uppercase;
}
```

<br />

(9) 가상클래스 is로 선택자 중복 줄이기

- `:before, :after` 단순하게 사용 할 경우 position 필요없음, 기본적으로 inline요소이기 때문에 크기값(`width, height`)을 가질수 없음 => 줄 바뀜(`display: block`), 줄 안바뀜(`display: inline-block`)

```scss
form {
  & :is(input[type="text"], input[type="email"], input[type="password"]) {
    ...;
  }
}
```

<br />

(10) 변수(Variables) - 01

- `$변수명: 값` => `선택자 { 속성: $변수명 }`
- 대시( `-` ), 언더바( `_` )를 제외하고 특수기호 또는 숫자로 변수명을 시작하면 안됨.

```javascript
제목(heading) + 색상(color) = $heading-color
제목(heading) + 색상(font-color) = $heading-fc
제목(heading) + 색상(background-color) = $heading-bgc
```

<br />

(11) 변수(Variables) - 02

```scss
$porfolio-images-url: "img/";

div {
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  background-image: url($porfolio-images-url + "blog-post-01.jpg");
}
```

<br />

(12) 변수(Variables) 유효범위와 데이터타입

- css에서 변수 var() 사용하기

```css
/* 
:root {
  --변수명: 값;
} 
*/

:root {
  --primary-color: #222;
  --secondary-color: #444;
}

.porfolio {
  color: var(--primary-color);
  color: var(--secondary-color);
}
```

<br />

(13) 외부파일 가져오기 @import

- `@import "파일명";`
  - "파일명"에는 확장자를 포함 시켜도 되고, 확장자를 제외하고 파일명만 사용해도 됨
    - `@import "reset";` ( O )
    - `@import "reset.scss";` ( O )

```scss
@import url("https://fonts.googleapis.com/css?family=Raleway&display=swap");

/* Reset.css */
@import url("reset.css"); // => scss파일에서 css파일 불러올때
@import "reset"; // => scss파일에서 scss파일 불러올때

body {
  font-family: "Raleway", sans-serif;
}
```

<br />

(14) @import로 분할(Partial)된 파일 불러오기

```scss
@import "header";
@import "footer";
@import "variables";
@import "fonts";

body {
  font-family: "Raleway", sans-serif;
  background-color: $body-bgc;
}
```

<br />

(15) 연산자(Operations), 출력창 없애기

- 산술연산자
  - SCSS에서도 calc를 사용할 수 있음 => css 컴파일 되면서 구문 그대로 출력되지만 css 코드에서는 역할을 함
  - `+` : 더하기
  - `-` : 빼기
  - `*` : 곱하기
  - `/` : 나누기⭐
    - 변수일 경우 => `margin: $box-margin / 2;`
    - 일반적인 경우 => 가로( `( )` ) 사용 및 나누는 대상 px 없앨 것 => `padding: ( 50px / 10 );` ⭐
  - `%` : 나머지

<br />

- 비교연산자
  - `==` : 동등
  - `!=` : 부등
  - `<` : 대소 / 보다 작은
  - `>` : 대소 / 보다 큰
  - `<=` : 대소 및 동등 / 보다 작거나 같은
  - `>=` : 대소 및 동등 / 보다 크커나 같은

<br />

- 논리연산자
  - `and` : 그리고
  - `or` : 또는
  - `not` : 부정

<br />

(16) ✨ 그룹 재사용 @mixin을 사용하기 @include

- @mixin : 재사용할 그룹을 선언(정의, 지정)하는 것
- @include : 정의된 @mixin을 사용(포함)하는 것

```scss
//SCSS 선언 방식
@mixin 믹스인_이름 {
  재사용 스타일 속성
}

//SCSS 사용 방식
선택자 {
  @include 믹스인_이름;
}

/*
//SASS 선언 방식
= 믹스인_이름 {
  재사용 스타일 속성
}

//SASS 사용 방식
선택자 {
  + 믹스인_이름;
}
*/
```

- `position : absolute;`에서 `bottom: 0;`으로 하고 부모의 `padding-bottom`으로 조절하는 것이 효율적

<br />

(17) 그룹 재사용 @mixin과 @include 응용하기

- `@mixin`은 따로 파일을 만든 후, `@import`해서 사용하는 것이 좋음

```scss
@import url("https://fonts.googleapis.com/css?family=Raleway&display=swap");

@import "mixin";

body {
  @include default;
}
```

<br />

(18) @mixin과 @include 활용한 버튼 디자인⭐

```scss
/* Button Design with @mixin and @include */
// Color & Font Variables
$complete-btn: royalblue;
$loading-btn: green;
$error-btn: crimson;
$notice-btn-hover: #000;
$notice-btn-fs: 18px;

// Button Mixin
@mixin notice-button {
  font-size: $notice-btn-fs;
  width: 150px;
  padding: 7px;
  background-color: #fff;
  outline: none;
  cursor: pointer;
  border-radius: 5px;
  transition: 0.35s;
  /* &:hover {
    background-color: $notice-btn-hover;
    color: #fff;
    border-color: transparent;
  } */
  &.complete:hover {
    background-color: $complete-btn;
    color: #fff;
    border-color: transparent;
  }
  &.loading:hover {
    background-color: $loading-btn;
    color: #fff;
    border-color: transparent;
  }
  &.error:hover {
    background-color: $error-btn;
    color: #fff;
    border-color: transparent;
  }
}

.complete {
  @include notice-button;
  border: 3px solid $complete-btn;
  color: $complete-btn;
}
.loading {
  @include notice-button;
  border: 3px solid $loading-btn;
  color: $loading-btn;
}
.error {
  @include notice-button;
  border: 3px solid $error-btn;
  color: $error-btn;
}
```

<br />

(19) @mixin의 매개변수(인자)를 @include로 사용하기⭐

```scss
//SCSS 사용 방식
@mixin 믹스인_이름($Parameter1, $Parameter2, $Parameter3) {
  css속성: $Parameter1 $Parameter2 $Parameter3;
}

@include 믹스인_이름(Argument1, Argument2, Argument3);
```

```scss
/* Arguments with @mixin and @include */
// Buttons Mixin
@mixin border-style($width, $style, $color) {
  border: $width $style $color;
}
@mixin button-padding($updown, $leftright) {
  padding: $updown $leftright;
}

.buttons {
  button {
    // width: 200px;
    padding: 7px;
    background-color: #fff;
    outline: none;
    cursor: pointer;
    font-size: 18px;
    @include button-padding(20px, 150px);
    &.approval {
      @include border-style(2px, solid, blue);
    }
    &.refuse {
      @include border-style(2px, dashed, red);
    }
  }
}
```

<br />

(20) 선택자 속성 가져오는 @extend

- 복사+붙여넣기
  1. 복상 대상 선택자
  2. @extend를 활용해 복사한 모든 CSS 속성 붙여넣기 + 추가 CSS 속성

```scss
//SCSS 선언 방식
@extend 선택자;

.btn {
  width: 200px;
  padding: 7px;
  background-color: #fff;
  font-size: 18px;
  text-transform: capitalize;
  border-radius: 5px;
  border-color: transparent;⭐
  outline: none;
  cursor: pointer;
  color: #fff;
  // border: 1px solid #000;
}
.order {
  @extend .btn;
  background-color: purple;
}
.add {
  @extend .btn;
  background-color: yellowgreen;
}
.checkout {
  @extend .btn;
  color: #000;
  border: 1px solid #000;⭐
}
```

<br />

(21) @extend와 함께 사용하는 플레이스 홀더 선택자(%)

- 컴파일 된 CSS 차이

```scss
/* % Keyword with @extend */
%shape {
  width: 250px;
  height: 300px;
  border-radius: 5px;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.212);
}

.card {
  display: flex;
  gap: 30px;
  &-item {
    @extend %shape;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
```

<br />

(22) - 다중 변수 선언, 내장 함수(map-get)

- Palettes | Flat UI Colors => 이쁜 색상 사이트⭐
- map-get(변수명, 키)
- 다중 변수 선언 => 세미콜론 마무리 할 것

```scss
/* Built-in Function : map-get */
$color: (
  font-primary: #2d3436,
  font-secondary: #636e72,
  font-focus: #d63031,
  bgc-primary: #dfe6e9,
  bgc-secondary: #b2bec3,
);
$headline-font: (
  large: 45px,
  medium: 32px,
  small: 22px,
);
$font-family: (
  kor: "Noto Sans KR",
  eng: "Montserrat",
);

body {
  background-color: map-get($color, bgc-primary);
  font-family: map-get($font-family, kor);
}
.frame {
  h1 {
    color: map-get($color, font-focus);
    font-size: map-get($headline-font, large);
    font-family: map-get($font-family, eng);
  }
  h2 {
    font-size: map-get($headline-font, medium);
  }
  h3 {
    font-size: map-get($headline-font, small);
  }
}
```

<br />

---

<br />

### ✨ 2. SCSS 핵심이론 활용 예제(Examples of using)

(1) 주요 CSS 선택자, 주요 가상클래스 활용하기

1. :link 방문하지 않은 링크 선택해 스타일 줄 때 사용
2. :visited 이미 방문한 링크를 선택해 스타일 줄 때 사용
3. :hover 마우스 커서를 올려놓을 때의 스타일 줄 때 사용
4. :active 클릭하고 띄지 않았을 때의 스타일 줄 때 사용

- ‼️ 주의 => :active 스타일은 반드시 :hover 스타일 뒤에 와야 합니다. :hover 앞에 오면 :hover 영향을 받게 됨

<br />

(2) @import로 reset.css와 normalize.css 연결하기

```SCSS
* {
  box-sizing: border-box;
}
a {
  text-decoration: none;
  color: #222;
}
button, input {
  outline: none;
}
button,
input[type=button],
input[type=submit],
input[type=reset] {
  cursor: pointer;
}
ol, ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
h1,h2,h3,h4,h5,h6 {
  font-weight: normal;
  margin-top: 0;
}
```

```SCSS
/* Import Reset CSS & Normalize CSS Style */
//  @import "reset";
//  @import "normalize";
 @import "custom-reset";
```

<br />

(3) @mixin을 중첩 활용해서 텍스트 서식 설정하기

```SCSS
@import url('https://fonts.googleapis.com/css?family=Raleway&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;500;700;900&display=swap');

$font-base: 15px;
$font-family-base: 'Raleway';
$font-family-headline: 'Roboto';

// Mixins
@mixin font-default {
  font: {
    size: $font-base;
    weight: 300;
    family: $font-family-base;
  }
  line-height: 1.6em;
}
@mixin font-headline {
  font: {
    family: $font-family-headline;
    weight: 500;
  }
  text-transform: uppercase;
}
@mixin large-headline {
  @include font-headline;
  font-size: $font-base * 3;
  color: crimson;
}

...

body {
  @include font-default;
}
h1 {
  @include large-headline;
}

...

```

<br />

(4) @mixin 배열(Array)에 인수 사용하고 @include로 인수 반환하기

```SCSS
@mixin 믹스인_이름(매개변수1, 매개변수2) {

}

@include 믹스인_이름(전달할_값1, 전달할_값2)
```

<br />

(5) 자주 사용하는 이펙트를 @mixin과 @include로 재사용

- `object-fit: cover;` : 요소의 가로나 세로크기에 가능한 맞춰져 크기가 조정되고, 비율은 고정된 상태. 개체 크기에 맞게 잘림. 가득 채울때까지 확대.
- `object-fit` 사용할 경우 `width`, `height` 값이 있어야 함⭐
- `object-fit`일 경우 `border-radius;`에 `overflow: hidden;` 추가해야 반영됨⭐

```SCSS
@mixin shadow-item {
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.35);
  // transform: translateY(-15px);
}

.items {
  display: flex;
  gap: 40px;
  > div {
    flex: 1;
    height: 400px;
    border-radius: 10px;
    overflow: hidden;
    transition: 0.35s;
    &:hover {
      @include shadow-item;
      transform: translateY(-15px);
    }
    a {
      width: inherit;
      height: inherit;
      img {
        object-fit: cover;
        width: inherit;
        height: inherit;
        // border-radius: 10px;
      }
    }
  }
}
```

<br />

(6) 특정 선택자 CSS 속성 가져오는 @extend를 활용해 CSS 디자인 재사용

```SCSS
.basic {
  border: none;
  background-color: transparent;
  text-transform: capitalize;
  font-weight: normal;
  font-size: 18px;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  outline: none;
  color: #fff;
  width: 150px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.16);
  transition: 0.35s;
  &:active {
    box-shadow: none;
  }
}
.success {
  @extend .basic;
  background-color: #2ecc71;
}
.error {
  @extend .basic;
  background-color: #f79f1f;
}
.warning {
  @extend .basic;
  background-color: #ee5a24;
}
.critical-error {
  @extend .basic;
  background-color: #ea2027;
}
```

<br />

(7) 플레이스 홀드(%) 선택자로 CSS 선택자를 연결선택자로 정리하기

```SCSS
/* Placeholder % */
%circle-box {
  border: 5px solid black;
  width: 200px;
  height: 200px;
  border-radius: 50%;
  display: inline-block;
}
.items {
  div {
    @extend %circle-box;
    &:nth-child(1) {
      background-color: red;
    }
    &:nth-child(2) {
      background-color: yellowgreen;
    }
    &:nth-child(3) {
      background-color: crimson;
    }
  }
}
```

<br />

(8) @mixin에 매개변수를 활용해서 다양한 Border Radius 만들기

- Border Radius : 좌측 상단 모서리를 기준으로 시계 방향으로 상 -> 우 -> 하 -> 좌
- `.box${square$}*8` => square 텍스트가 들어가있는 `<div class="box(1~8)"> square(1~8) <div>` 8개 생성⭐
- `display: flex;`에서 기본값은 `flex-wrap: nowrap;`이기 때문에 item의 width값을 유지하지 못함 => `flex-wrap: wrap;`으로 바꾸면 item의 width값이 유지됨⭐

```SCSS
@mixin bdrs($radius) {
  border-radius: $radius;
}

...

&:nth-child(6) {
    @include bdrs(50% 50% 50% 0);
  }
```

<br />

(9) SCSS에서 부모요소 참조해서 만드는 일관성 있는 html 레이아웃 구조

```SCSS
.vision {
  display: flex;
  &-inner {
    width: 1200px;
    overflow: hidden;
  }
  &-content {
    width: 100%;
    height: 200px;
    > div {
      float: left;
      width: 100%;
    }
  }
  &-item {
    height: 200px;
    &-desc {
      background-color: red;
      h1 {
        text-align: center;
      }
    }
  }
}
```

<br />

---

<br />

### ✨ 3. SCSS+GRID+FLEX+실전+포트폴리오+퍼블리싱

(1) 가상클래스로 활용한 살아있는 애니메이션 하트

```SCSS
.heart-beat {
  width: 100px;
  height: 100px;
  position: relative;
  background-color: #ff4757;
  transform: rotate(45deg);
  box-shadow: 0 -10px 100px #ff4757,
              0 -10px 150px #ff4757,
              0 -10px 200px #ff4757;
  animation: heart-beat 0.5s linear infinite;
  &:before,
  &:after {
    content: '';
    position: absolute;
    width: inherit;
    height: inherit;
    border-radius: 50%;
    background-color: inherit;
  }
  &:before {
    top: -50%;
  }
  &:after {
    left: -50%;
  }
}
@keyframes heart-beat {
  0% {
    transform: rotate(45deg) scale(1);
  }
  50% {
    transform: rotate(45deg) scale(1.05);
  }
  100% {
    transform: rotate(45deg) scale(0.95);
  }
}
```

<br />

---

<br />
