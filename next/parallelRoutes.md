# Parallel Routes(병렬 라우트)

nextjs 13버전에서 등장한 라우트 방식이다.

예를들면 A라는 페이지와 B라는 페이지가 있는데

이를 동시에 렌더링해서 한 화면에 보여줄수도 있다.

A와 B의 각각의 상황에 따라 오류라던지 로드 상태도 정의 가능하다.

인증 상태라던가 조건이 있다면 그에 따라 렌더링 처리도 가능해진다.

<h2>Convention</h2>

병렬 라우트를 쓸려면 이름이 명시된 슬롯을 사용해야된다.(원문 : Parallel routes are created using named slots.)

슬롯은 규칙에 의해 정의가 되며 props와 동일한 레이아웃에 전달된다.

```ts
export default function Layout(props: {
  children: React.ReactNode
  analytics: React.ReactNode
  team: React.ReactNode
}) {
  return (
    <>
      {props.children}
      {props.team}
      {props.analytics}
    </>
  )
}
```

여기서 children은 매핑할 필요가 없는 암시적 슬롯임

(처음에 프로젝트를 생성하면 기본으로 들어가 있는 슬롯)

<h2>Unmatched Routes</h2>

매칭이 안되는 라우트일 경우

default.js

Nextjs가 슬롯 상태를 복구를 못하면 대체되는 파일이다.

단 대체파일조차 없을경우에는 404 에러가 불러와진다.

<h2>useSelectedLayoutSegment</h2>

useSelectedLayoutSegment, useSelectedLayoutSegments

모두 parallelRoutesKey를 받아들여 해당 슬롯 내에서 활성 라우트 세그먼트를 읽을 수 있도록 합니다.

```ts
'use client'
 
import { useSelectedLayoutSegment } from 'next/navigation'
 
export default async function Layout(props: {
  //...
  auth: React.ReactNode
}) {
  const loginSegments = useSelectedLayoutSegment('auth')
  // ...
}
```

@authModal/login 또는 URL 표시줄의 /login으로 이동하면 loginSegments는 문자열 login과 같음


Parallel Routes로 modal을 사용하는 예제가 공식문서에도 있긴한데

필요할때 보면 될거 같고

Parallel Routes는 많은 정보를 표시하는 대시보드

같은 페이지 url이지만 권한에 따라 다르게 보여야 할 경우

카테고리별로 보여줘야할 데이터를 한페이지에 표시해야되는 경우 등등..

다양한곳에서 쓸수 있을거 같다.