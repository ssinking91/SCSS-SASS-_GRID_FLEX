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
- `:before :after` 태그는 inline 속성이기때문에 크기 값을 가질수 없음 => position : absolute가 되면 모든 요소는 인라인 블록으로 display 속성이 변함

(3) 부모 선택자 참조 응용

- `class="font-large"` => `.font {&-large{ ... }}`

(4) 대표적인 CSS 선택자 SCSS에서 만들기

- 태그와 함께쓰는 선택자 : `p.center{ ... }` => p와 .center 사이 띄어쓰기 하지 말것⭐
- 그룹선택자 : `h1,p span{ ... }` => 콤마(,)로 연결, 연결 선택자라고도 함⭐
- 공통적으로 사용 할 UI는 부모요소 밖에서 CSS를 하여 재사용이 가능하도록 만들것

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
