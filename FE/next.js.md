# next.js

- [next/link](#nextlink)
- [next/router](#nextrouter)

<br>

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
