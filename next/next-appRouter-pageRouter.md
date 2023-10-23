# App Router와 Pages Router 차이점 및 비교

사내에서 개발중인 프로젝트가 Pages Router 방식으로 되어있다.<br/>
App Router로 전환되면 기존보다 이점이 많다는 이야기를 들었고 이에 대해 알아볼려는게 목적<br/>

스택오버플로우에 누군가가 올려놓은 간략한 비교이다.

| Feature                       | App Router     | Pages Router  |
|-------------------------------|----------------|---------------|
| Routing type                  | Server-centric | Client-side   |
| Support for Server Components | Yes            | No            | 
| Complexity                    | More complex   | Simpler       | 
| Performance                   | Better         | Worse         |
| Flexibility                   | More flexible  | Less flexible |

그리고 Next 공식문서에 이런 내용이 있다.<br/>

```
App Router와 Page Router

Next.js에는 앱 라우터(App Router)와 페이지 라우터(Pages Router)라는 두 가지 라우터가 있습니다.<br/>
앱 라우터는 서버 구성 요소 및 스트리밍과 같은 React의 최신 기능을 사용할 수 있는 최신 라우터입니다.<br/>
Pages Router는 서버에서 렌더링된 React 애플리케이션을 구축할 수 있게 해 주고<br/>
이전 Next.js 애플리케이션에 대해 계속 지원되는 최초의 Next.js 라우터입니다.

계속 나올 최신 기능들을 쓰고싶으면 App Router를 써야한다는것으로 보여진다.
```
## 폴더 구조의 차이

기존의 Page Router에서는 pages 폴더 안에 pages/index.tsx와 같이 만들어서 사용하면 되었으나<br/>
App Router에서는 폴더명으로 경로를 정의하며 page.tsx 또는 route.tsx로 작성된 파일만 가능하다.

pages/index.tsx → /app/page.tsx <br/>
pages/dashboard/index.tsx → /app/dashboard/page.tsx<br/>
pages/contents/index.tsx → /app/contents/page.tsx

## 랜더링

랜더링도 개선되서 속도가 빨라진다고 되어있는데
실제로 라우터 변경 작업하면서 상세히 알아볼 예정