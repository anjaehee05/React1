# 컴포넌트 import 및 export 하기

컴포넌트의 가장 큰 장점은 재사용성으로 컴포넌트를 조합해 또 다른 컴포넌트를 만들 수 있다는 것입니다. 컴포넌트를 여러 번 중첩하게 되면 다른 파일로 분리해야 하는 시점이 생깁니다. 이렇게 분리하면 나중에 파일을 찾기 더 쉽고 재사용하기 편리해집니다.

## Root 컴포넌트란

첫 컴포넌트에서 만든 `Profile` 컴포넌트와 `Gallery` 컴포넌트는 아래와 같이 렌더링 됩니다. 이 예시의 컴포넌트들은 모두 `App.js`라는 root 컴포넌트 파일에 존재합니다. 설정에 따라 root 컴포넌트가 다른 파일에 위치할 수도 있습니다. Next.js처럼 파일 기반으로 라우팅하는 프레임워크일 경우 페이지별로 root 컴포넌트가 다를 수 있습니다.

## 컴포넌트를 import 하거나 export 하는 방법

랜딩 화면을 변경하게 되어 과학자들이 아니라 과학책으로 변경되거나 프로필 사진을 다른 곳에서 사용하게 된다면 `Gallery` 컴포넌트와 `Profile` 컴포넌트를 root 컴포넌트가 아닌 다른 파일로 옮기는 게 좋습니다. 그렇게 변경하면 재사용성이 높아져 컴포넌트를 모듈로 사용할 수 있습니다.

컴포넌트를 다른 파일로 이동하려면 세 가지 단계가 있습니다.

1. 컴포넌트를 추가할 JS 파일을 생성합니다.
2. 새로 만든 파일에서 함수 컴포넌트를 export 합니다. (default 또는 named export 방식을 사용합니다)
3. 컴포넌트를 사용할 파일에서 import 합니다. (적절한 방식을 선택해서 default 또는 named로 import 합니다)

> **중요합니다!**
> 가끔 `.js`와 같은 파일 확장자가 없을 때도 있습니다.

## 한 파일에서 여러 컴포넌트를 import 하거나 export 하는 방법

전체 갤러리가 아니라 하나의 `Profile`만 사용하고 싶을 때 `Profile` 컴포넌트만 export 하면 됩니다. 하지만 `Gallery.js` 파일에는 이미 하나의 default export가 존재하기 때문에 두 개의 default export를 정의할 수 없습니다. 이런 경우 새로운 파일 하나를 더 생성해서 default export를 사용하거나 named export로 `Profile` 컴포넌트를 export 할 수 있습니다.

한 파일에서는 단 하나의 default export만 사용할 수 있지만 named export는 여러 번 사용할 수 있습니다.

먼저 named export 방식을 사용해서 `Gallery.js` 파일에서 `Profile` 컴포넌트를 export 합니다. (`default` 키워드를 사용하지 않습니다)

```js
export function Profile() {
  // ...
}
```

그 다음엔 named import 방식으로 `Gallery.js` 파일에서 `Profile` 컴포넌트를 `App.js` 파일로 import 합니다. (중괄호를 사용합니다)

```js
import { Profile } from "./Gallery.js";
```

마지막으로 `<Profile />`을 `App` 컴포넌트에서 렌더링합니다.

```js
export default function App() {
  return <Profile />;
}
```

이제 `Gallery.js`에는 default `Gallery` export랑 named `Profile` export라는 두 가지의 export가 존재합니다. `App.js`에서는 두 컴포넌트를 import 해서 사용합니다.
