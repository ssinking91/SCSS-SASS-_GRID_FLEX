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
      "savePath": null,
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

<br />

---

<br />

### ✨ 1. SCSS 핵심 이론(Essential Theory)

(1) 선택자 중첩(Nesting)

- body는 독립적으로 => reset으로 사용

(2) 부모 선택자 참조(&)와 주석⭐

- &(Ampersand) = 부모요소 선택자
- 주석 = `/* */` or `//`
- `a` 태그는 inline 속성이기때문에 크기 값을 가질수 없음 => display : block / inline-block
- `:before :after` 태그는 inline 속성이기때문에 크기 값을 가질수 없음 => position : absolute가 되면 모든 요소는 inline-block으로 display 속성이 변함것⭐

(3) 부모 선택자 참조 응용

- `class="font-large"` => `.font {&-large{ ... }}`

(4) 대표적인 CSS 선택자 SCSS에서 만들기

- 태그와 함께쓰는 선택자 : `p.center { ... }` => p와 .center 사이 띄어쓰기 하지 말것⭐
- 그룹선택자 : `h1,p span { ... }` => 콤마(,)로 연결, 연결 선택자라고도 함⭐
- 공통적으로 사용 할 UI는 부모요소 밖에서 CSS를 하여 재사용이 가능하도록 만들것

(5) 부모 선택자 참조, 가상클래스

- 가상클래스 `&:hover, &:nth-child(n), &:first-child, &:before, &:after, &::placeholder`등 &와 연결해서 사용
- 아이디, 클래스 속성선택자 `&#id-name, &.class-name, &[type-radio]`등 &와 연결해서 사용
- `body {font-family:...}`는 input태그에 적용되지 않음 => `* {font-family:...}`로 변경것⭐
- `button`태그는 `transition: 0.35s`가 가장 적당함것⭐

(6) 부모 선택자 참조, 속성선택자

- `<input type="button">` => `선택자[속성="값"] {...}`
- `<input type="button" value="텍스트 내용">`
- `input`, `button`태그는 display: inline-block 기본요소 => display: block을 하더라도 width: 100% 를 주어야 함⭐

(7) 부모선택자 중첩 나가기 @at-root

- `@ : 골뱅이(at sign)`
- `& : 앰퍼샌드(ampersand)`
- `~ : 물결(tild)`
- `^ : 눈꼬리(caret)`

(8) 접두어(prefix) 사용해서 CSS 속성 자동생성

```css
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

---

<br />

### ✨ 2. SCSS 핵심이론 활용 예제(Examples of using)

<br />

---

<br />

### ✨ 3. SCSS+GRID+FLEX+실전+포트폴리오+퍼블리싱

<br />

---

<br />
