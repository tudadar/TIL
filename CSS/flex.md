# flex

기본적인 사용법은

display 속성에 flex를 지정하면된다.

모질라 재단의 css flex에 대한 문서를 보면

```
flex CSS 속성은 하나의 플렉스 아이템이 자신의 컨테이너가 차지하는 공간에 맞추기 위해 크기를 키우거나 줄이는 방법을 설정하는 속성입니다.
flex는 flex-grow, flex-shrink, flex-basis의 단축 속성입니다.
```

여기서 단축속성이라는 단어가 생소했는데 생각해보니

흔히 많이들 쓰는 margin 속성을 생각하면 쉽게 이해가 되었다.

```css
/* Keyword values */
flex: auto;
flex: initial;
flex: none;

/* One value, unitless number: flex-grow */
flex: 2;

/* One value, length or percentage: flex-basis */
flex: 10em;
flex: 30%;

/* Two values: flex-grow | flex-basis */
flex: 1 30px;

/* Two values: flex-grow | flex-shrink */
flex: 2 2;

/* Three values: flex-grow | flex-shrink | flex-basis */
flex: 2 2 10%;

/* Global values */
flex: inherit;
flex: initial;
flex: unset;
```

```
flex 속성은 한 개에서 세 개의 값을 사용해 지정할 수 있습니다.

값이 한 개일 때, 그 값은 다음 중 하나여야 합니다.
<number>를 지정하면 <flex-grow>입니다.
<length> 또는 <percentage>를 지정하면 <flex-basis>입니다.
none, auto, initial 중 하나를 지정할 수 있습니다.
값이 두 개일때, 첫 번째 값은 <number>여야 하며 <flex-grow>가 됩니다. 두 번째 값은 다음 중 하나여야 합니다.
<number>를 지정하면 <flex-shrink>입니다.
<length>, <percentage>, 또는 auto를 지정하면 <flex-basis>입니다.
값이 세 개일 때는 다음 순서를 따라야 합니다.
<flex-grow> 에 사용할 <number>
<flex-shrink> 에 사용할 <number>
<flex-basis> 에 사용할 <length>, <percentage>, 또는 auto
```

위와 같은 flex 속성을 사용하는 법을 이해해야 하고

아래의 속성들도 알고 이해한후 사용하여야한다.

```
flex-basis
flex-direction
flex-flow
flex-grow
flex-shrink
flex-wrap
```

참고자료 : https://developer.mozilla.org/ko/docs/Web/CSS/flex