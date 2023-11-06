# CSS Grid 사용하기

 기본적으로 그리드를 사용할려면

```css
 .container {
  display: grid;
}
```

이와 같이 display: grid; 를 선언해주면 된다.

```css
.container {
  display: grid;
  grid-template-columns: 200px 200px 200px;
}
```

이는 200px의 div 3개가 나란히 정렬된다.

만약 container 안에 7개의 div가 있다면

마지막 1개는 마지막줄에 혼자 표시된다.

길이 대신에 백분율(%)를 활용해서 정렬해도 된다.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
```

fr 단위를 활용해서 정렬할수도 있다.

fr은 공간을 비례적으로 분배해서 행과 열의 크기를 화면의 크기에 따라 유연하게 조정된다.

```css
.container {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
}
```

이런식으로 한쪽의 수치를 높게 줘서 첫번째가 더 커지게 분배할수도 있다.

```css
.container {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  grid-gap: 20px;
}
```

grid-gap 속성을 활용하면 상하로 div사이에 간격을 줄수가 있다.

단 fr은 사용할수 없고 px과 같은 단위와 %로만 가능하다.

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 100px;
  grid-gap: 20px;
}
```

grid-auto-rows는 그리드로 생성된 div의 높이를 지정해주는 역활을 한다.

해당값이 없으면 자동으로 맞춰짐

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: minmax(100px, auto);
  grid-gap: 20px;
}
```

minmax함수는 최소,최대 크기를 지정할수 있다.

최소크기는 100px 최대는 auto(자동)이다.


```css
header {
  grid-column: 1 / 3;
  grid-row: 1;
}

article {
  grid-column: 2;
  grid-row: 2;
}

aside {
  grid-column: 1;
  grid-row: 2;
}

footer {
  grid-column: 1 / 3;
  grid-row: 3;
}

body {
  width: 90%;
  max-width: 900px;
  margin: 2em auto;
  font:
    0.9em/1.2 Arial,
    Helvetica,
    sans-serif;
}

.container {
  display: grid;
  grid-template-columns: 1fr 3fr;
  gap: 20px;
}

header,
footer {
  border-radius: 5px;
  padding: 10px;
  background-color: rgb(207, 232, 220);
  border: 2px solid rgb(79, 185, 227);
}

aside {
  border-right: 1px solid #999;
}
```

```css
.container {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar content"
    "footer footer";
  grid-template-columns: 1fr 3fr;
  gap: 20px;
}

header {
  grid-area: header;
}

article {
  grid-area: content;
}

aside {
  grid-area: sidebar;
}

footer {
  grid-area: footer;
}

body {
  width: 90%;
  max-width: 900px;
  margin: 2em auto;
  font:
    0.9em/1.2 Arial,
    Helvetica,
    sans-serif;
}

header,
footer {
  border-radius: 5px;
  padding: 10px;
  background-color: rgb(207, 232, 220);
  border: 2px solid rgb(79, 185, 227);
}

aside {
  border-right: 1px solid #999;
}
```

위 2개의 css는 페이지를 확인해보면 똑같다.

두번재 css처럼 요소들에 이름을 지정하여 사용하는 방법도 있다.

css에 쓰인 grid-column, grid-row 요소는 아래를 참고

https://developer.mozilla.org/en-US/docs/Web/CSS/grid-column

https://developer.mozilla.org/en-US/docs/Web/CSS/grid-row

이번 그리드는 모질라 재단의 css 공식문서를 참고하였음

https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Grids

원래는 flex에 대해 먼저 봤었는데 못적었음

다음엔 flex에 대해서 적겠다.