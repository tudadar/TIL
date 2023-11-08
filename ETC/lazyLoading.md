# Lazy Loading

<h1>Lazy Loading의 정의</h1>

페이지 로딩시 당장 필요하지 않은 리소스를 나중에 불러오는것

필요한건 바로 불러오고 아닌것은 나중에 불러온다.

<h2>Code Splitting</h2>

JavaScript, CSS, HTML은 더 작은 코드로 분할될 수 있다.

페이지의 필요한 최소한의 코드를 먼저 불러오고 나머지는 요청시 불러올수 있게된다.

```
진입점 분할(Entry point splitting): 앱의 진입점별로 코드를 분리
동적 분할(Dynamic splitting): 동적인 import()문이 사용되는 코드를 분리
```

<h2>Javascript</h2>

type="module" 이 있는 모든 스크립트 태그는 JavaScript 모듈로 처리되며 기본적으로 지연처리됩니다.

<h2>css</h2>

기본적으로 CSS는 렌더링 차단 리소스로 처리되므로 브라우저는 CSSOM이 구성될 때까지 처리된 콘텐츠를 렌더링하지 않습니다.<br/>
CSS는 가벼워야하고 가능한 한 빨리 전달되어야 하며 미디어 유형 및 쿼리는 렌더링 차단을 해제하는 것이 좋습니다.

보다 상세한 예시는 아래에 있습니다.

https://web.dev/articles/critical-rendering-path/render-blocking-css?hl=ko

<h2>font</h2>

기본적으로 글꼴 요청은 렌더링 트리가 구성될 때까지 지연되므로 텍스트 렌더링이 지연될 수 있습니다.

```<link rel="preload">``` CSS font-display property 및 Font Loading API를 사용하여 기본 동작을 재정의하고 Web Font 리소스를 미리 로드할 수 있습니다.

<h2>이미지나 동영상</h2>

https://web.dev/articles/lazy-loading?hl=ko





참고한 링크

https://developer.mozilla.org/en-US/docs/Web/Performance/Lazy_loading