# app router

- [app router](#app-router)
- [next/link](#nextlink)
- [next/router](#nextrouter)

<br>

## app router

Next.js 13 버전에서는 React Server Components를 기반으로 한 새로운 App Router가 도입되었습니다. 이 App Router는 공유 레이아웃, 중첩 라우팅, 로딩 상태 처리, 에러 처리 등 다양한 기능을 지원합니다.

App Router는 "app"이라는 새 디렉토리에서만 작동합니다. 이 새 디렉토리는 기존의 "pages" 디렉토리와 함께 사용되며, 점진적으로 App Router로 바뀔 수 있도록 복수 지원합니다. 이를 통해 기존의 "pages" 디렉토리를 사용하던 기능과 함께 새로운 App Router를 사용하는 기능을 혼용할 수 있습니다. 다만, 두 가지 라우팅 방식이 같은 경로를 가지고 있다면 충돌을 방지하기 위해 빌드 타임에 App Router이 Pages Router보다 우선적용됩니다.

## 파일 기반 라우트

Next.js는 파일 시스템 기반의 라우터를 사용합니다. 이때 폴더는 라우트를 정의하는 데 사용됩니다.

![route](https://nextjs.org/_next/image?url=%2Fdocs%2Flight%2Froute-segments-to-path-segments.png&w=1920&q=75&dpl=dpl_3guogY6YECQnnD8P1bp8UJe7CDCH)

각 폴더는 URL segment 에 매핑되는 라우트 segment 를 나타냅니다.

## 파일 컨벤션

Next.js는 중첩된 라우트에서 특정 동작을 가진 UI를 만들기 위해 다음과 같은 파일 컨벤션을 제공합니다.

- layout: segment 와 그 자식들을 위한 공유 UI를 생성합니다.
- page: 라우트의 고유한 UI를 생성하며 라우트를 공개적으로 접근 가능하게 합니다.
- loading: segment 와 그 자식들을 위한 로딩 UI를 생성합니다.
- not-found: segment 와 그 자식들을 위한 찾을 수 없음 UI를 생성합니다.
- error: segment 와 그 자식들을 위한 에러 UI를 생성합니다.
- global-error: 전역 에러 UI를 생성합니다.
- route: 서버 측 API 엔드포인트를 생성합니다.
- template: 특수화된 다시 렌더링되는 레이아웃 UI를 생성합니다.
- default: 병렬 라우트를 위한 대체 UI를 생성합니다.

특수 파일 이외에도, 자신이 생성한 파일(예: 컴포넌트, 스타일, 테스트 등)들을 app 디렉토리의 폴더 안에 함께 배치할 수 있습니다.

## 컴포넌트 계층 구조

파일 컨벤션에서 정의된 React 컴포넌트들은 다음과 같은 특정한 계층 구조로 렌더링됩니다.

![컴포넌트 계층 구조](https://nextjs.org/_next/image?url=%2Fdocs%2Flight%2Ffile-conventions-component-hierarchy.png&w=1920&q=75&dpl=dpl_Ev1SSnkTzSfmJGJRmYbn4JZhjkvm)

1. layout.js
2. template.js
3. error.js (React 에러 바운더리)
4. loading.js (React 서스펜스 바운더리)
5. not-found.js (React 에러 바운더리)
6. page.js 또는 중첩된 layout.js

중첩 라우트의 경우, 자식 segment의 컴포넌트들은 부모 segment의 컴포넌트들 안에 중첩됩니다.

![중첩 컴포넌트 계층](https://nextjs.org/_next/image?url=%2Fdocs%2Flight%2Fnested-file-conventions-component-hierarchy.png&w=1920&q=75&dpl=dpl_Ev1SSnkTzSfmJGJRmYbn4JZhjkvm)

## next/link

`<a>` 태그를 사용하여 링크를 이동하면, 일반적으로 해당 링크 페이지에 대한 정보를 사전에 가져오지 않고 이동했을 때 새로운 HTML을 받아와야 합니다.

`next/link`를 사용하면 링크가 생성된 페이지에 대한 정보를 사전에 가져와 JavaScript 파일로 미리 로드합니다. 이를 통해 페이지 이동 전에 필요한 데이터를 사전에 가져와서 클라이언트 측에서 부분적으로 CSR과 유사한 방식으로 처리할 수 있습니다. 또한, `next/link`를 사용하여 생성된 링크 페이지에 대한 HTML은 서버에서 프리렌더링되므로 CSR과 유사한 동작을 하더라도 SEO 측면에서 문제가 발생하지 않습니다.

- 사용법

```javascript
import Link from "next/link";

// <Link href="/링크경로">링크이름</Link>;
<Link href="/section1/getStaticProps">/getStaticProps</Link>;
```

![image-20230713231356303](https://raw.githubusercontent.com/ddullgi/image_sever/master/img/image-20230713231356303.png)

렌더링 후 element 상에서는 `<a>`태그로서 동작한다.

#### 스크롤에 따른 지연 로딩

`next/link`는 스크롤 위치에 따라 프리로딩을 지연하는 기능을 기본적으로 제공하여 사용자가 스크롤을 통해 특정 영역에 도달할 때까지 필요한 데이터를 프리로드하지 않고, 필요한 순간에 로드하여 효율적인 성능을 제공합니다. 이는 대규모 페이지나 많은 링크가 있는 경우 유용할 수 있으며, 사용자 경험과 초기 로딩 속도를 개선할 수 있습니다.

```javascript
import Link from "next/link";

export default function Links() {
  return (
    <main>
      <h1>Links</h1>
      <div style={{ height: "200vh" }}></div>
      <Link href="/section1/getStaticProps">/getStaticProps</Link>
    </main>
  );
}
```

위 코드와 같이 `<Link>`태그를 페이지에 보이는 영역 바깥에 위치하게 될 경우 `<Link>`태그가 보이지 않을 때는 링크 페이지가 프리로드되지 않다가 해당 영역에 스크롤이 닿았을 때 프리로드 됩니다.

![image-20230713222227408](https://raw.githubusercontent.com/ddullgi/image_sever/master/img/image-20230713222227408.png)
![image-20230713222247138](https://raw.githubusercontent.com/ddullgi/image_sever/master/img/image-20230713222247138.png)

> #### 주의할 점
>
> next 프로젝트를 dev 환경에서 실행할 경우 프리로딩이 수행되지 않고 클릭했을 때 실행된다는 점을 인지하고 있어야합니다.

## next/router

> [next/link](#nextlink)의 내용 참고

`next/router`는 Next.js에서 제공하는 라우팅 관련 기능을 사용할 수 있는 모듈입니다. `next/link`와 비슷한 역할을 하지만 프리렌더링 기능은 제공하지 않습니다.

- 사용법

```jsx
import { useRouter } from "next/router";

export default function Links() {
  const router = useRouter();

  return (
    <button
      onClick={() => {
        router.push("/section1/getStaticProps");
      }}
    >
      /getStaticProps
    </button>
  );
}
```

`const router = useRouter();`를 선언한 후 onClick에 콜백 함수로 페이지 링크를 push 해주면됩니다.
