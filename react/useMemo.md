# useMemo

우선 공식문서를 보면

useMemo는 리렌더링 사이의 계산 결과를 캐시할 수 있는 React Hook

이라고 명시되어있다.

Memo 는 "memoized" 를 의미하는데 이전에 계산 한 값을 재사용한다는 의미이고

메모한다의 메모가 아닙니다.

```ts
import React, { useMemo } from 'react';

function MyComponent({ data }) {
  const processedData = useMemo(() => {
    // Expensive computation or data transformation
    return processData(data);
  }, [data]);

  // Render the component using processedData

  return <div>{processedData}</div>;
}

```

이런식으로 사용하게되면 계산한 결과를 기억했다가 쓸대없는 재계산을 방지해서

성능적인 면에서 도움이 될꺼라 보여진다.

사실 useState나 useEffect 같은 hook은 많이 쓰기도 하고 봐와서 익숙한데

useMemo는 실제 사용되는 경우는 계산과정이 복잡하고 오래걸리는게 아니면 사용 할일이 없어보인다.

성능적인 면에서 문제가 있는 경우가 아니면 사용 안하는게 좋을걸로 보여진다.