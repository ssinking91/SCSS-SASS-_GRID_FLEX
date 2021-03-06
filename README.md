### ๐ซ SCSS-SASS-\_GRID_FLEX

<br />

---

<br />

### โ๏ธ Live Sass Compiler ์ค์ 

```javascript
vscode => setting.json

{
  // ์ปดํ์ผ ํฌ๋งท ๋ฐฉ์ ์์ฑ
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

  // map ํ์ผ ์ฌ์ฉ ์ ๋ฌด(Default : true) - ์์ค๋งต ์ฌ์ฉ์ํ  ๊ฒฝ์ฐ false๋ก ์ค์ 
  "liveSassCompile.settings.generateMap": false,

  // ์๋ ๋ฐด๋ ํ๋ฆฌํฝ์ค ์ฌ์ฉํ๊ฒ ํด์ค.
  "liveSassCompile.settings.autoprefix": ["> 1%", "last 2 versions"]
  // "liveSassCompile.settings.autoprefix": null
}
```

<br />

---

<br />

### โจ 1. SCSS ํต์ฌ ์ด๋ก (Essential Theory)

(1) ์ ํ์ ์ค์ฒฉ(Nesting)

- body๋ ๋๋ฆฝ์ ์ผ๋ก => reset์ผ๋ก ์ฌ์ฉ

(2) ๋ถ๋ชจ ์ ํ์ ์ฐธ์กฐ(&)์ ์ฃผ์โญ

- &(Ampersand) = ๋ถ๋ชจ์์ ์ ํ์
- ์ฃผ์ = `/* */` or `//`
- `a` ํ๊ทธ๋ inline ์์ฑ์ด๊ธฐ๋๋ฌธ์ ํฌ๊ธฐ ๊ฐ์ ๊ฐ์ง์ ์์ => display : block / inline-block
- `:before :after` ํ๊ทธ๋ inline ์์ฑ์ด๊ธฐ๋๋ฌธ์ ํฌ๊ธฐ ๊ฐ์ ๊ฐ์ง์ ์์ => position : absolute๊ฐ ๋๋ฉด ๋ชจ๋  ์์๋ inline-block์ผ๋ก display ์์ฑ์ด ๋ณํจ๊ฒโญ

(3) ๋ถ๋ชจ ์ ํ์ ์ฐธ์กฐ ์์ฉ

- `class="font-large"` => `.font {&-large{ ... }}`

(4) ๋ํ์ ์ธ CSS ์ ํ์ SCSS์์ ๋ง๋ค๊ธฐ

- ํ๊ทธ์ ํจ๊ป์ฐ๋ ์ ํ์ : `p.center { ... }` => p์ .center ์ฌ์ด ๋์ด์ฐ๊ธฐ ํ์ง ๋ง๊ฒโญ
- ๊ทธ๋ฃน์ ํ์ : `h1,p span { ... }` => ์ฝค๋ง(,)๋ก ์ฐ๊ฒฐ, ์ฐ๊ฒฐ ์ ํ์๋ผ๊ณ ๋ ํจโญ
- ๊ณตํต์ ์ผ๋ก ์ฌ์ฉ ํ  UI๋ ๋ถ๋ชจ์์ ๋ฐ์์ CSS๋ฅผ ํ์ฌ ์ฌ์ฌ์ฉ์ด ๊ฐ๋ฅํ๋๋ก ๋ง๋ค๊ฒ

(5) ๋ถ๋ชจ ์ ํ์ ์ฐธ์กฐ, ๊ฐ์ํด๋์ค

- ๊ฐ์ํด๋์ค `&:hover, &:nth-child(n), &:first-child, &:before, &:after, &::placeholder`๋ฑ &์ ์ฐ๊ฒฐํด์ ์ฌ์ฉ
- ์์ด๋, ํด๋์ค ์์ฑ์ ํ์ `&#id-name, &.class-name, &[type-radio]`๋ฑ &์ ์ฐ๊ฒฐํด์ ์ฌ์ฉ
- `body {font-family:...}`๋ inputํ๊ทธ์ ์ ์ฉ๋์ง ์์ => `* {font-family:...}`๋ก ๋ณ๊ฒฝ๊ฒโญ
- `button`ํ๊ทธ๋ `transition: 0.35s`๊ฐ ๊ฐ์ฅ ์ ๋นํจ๊ฒโญ

(6) ๋ถ๋ชจ ์ ํ์ ์ฐธ์กฐ, ์์ฑ์ ํ์

- `<input type="button">` => `์ ํ์[์์ฑ="๊ฐ"] {...}`
- `<input type="button" value="ํ์คํธ ๋ด์ฉ">`
- `input`, `button`ํ๊ทธ๋ display: inline-block ๊ธฐ๋ณธ์์ => display: block์ ํ๋๋ผ๋ width: 100% ๋ฅผ ์ฃผ์ด์ผ ํจโญ

(7) ๋ถ๋ชจ์ ํ์ ์ค์ฒฉ ๋๊ฐ๊ธฐ @at-root

- `@ : ๊ณจ๋ฑ์ด(at sign)`
- `& : ์ฐํผ์๋(ampersand)`
- `~ : ๋ฌผ๊ฒฐ(tild)`
- `^ : ๋๊ผฌ๋ฆฌ(caret)`

(8) ์ ๋์ด(prefix) ์ฌ์ฉํด์ CSS ์์ฑ ์๋์์ฑ

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

### โจ 2. SCSS ํต์ฌ์ด๋ก  ํ์ฉ ์์ (Examples of using)

<br />

---

<br />

### โจ 3. SCSS+GRID+FLEX+์ค์ +ํฌํธํด๋ฆฌ์ค+ํผ๋ธ๋ฆฌ์ฑ

<br />

---

<br />
