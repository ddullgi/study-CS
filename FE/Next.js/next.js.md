# next.js

- [서버 컴포넌트와 클라이언트 컴포넌트](#서버-컴포넌트와-클라이언트-컴포넌트)
- [next/link](#nextlink)
- [next/router](#nextrouter)
- [next/image](#nextimage)

<br>

## 서버 컴포넌트와 클라이언트 컴포넌트

![서버컴포넌트와 클라이언트 컴포넌트](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/6341/13043.png)

nextjs의 컴포넌트는 크게 server component와 client component로 구분됩니다. 특별한 처리를 하지 않으면 nextjs에서 컴포넌트는 server component 입니다.

![넥스트 서버 클라이언트 컴포넌트 비교](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/6341/13053.png)

위의 그림을 보면 S가 server, C가 client component의 사용 사례를 보여줍니다.

서버 컴포넌트는 아래와 같은 경우에 사용합니다.

사용자와 상호작용하지 않는 경우
백엔드에 엑세스하면서 보안적으로 위험한 정보를 주고 받는 경우
클라이언트 컴포넌트는 아래와 같은 경우 사용합니다.

서버 컴포넌트로 해결되지 않는 경우
사용자와 상호작용하는 경우
useEffect, useState, onClick, onChange와 같은 API를 사용해야 하는 경우
useRouter, useParams와 같은 nextjs의 client component API를 사용하는 경우

아래는 nextjs의 구분법입니다.

![그림](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/6341/13050.png)

## next/link

`<a>` 태그를 통해 링크를 이동하면, 대게 해당 페이지에 대한 정보를 미리 가져오지 않고 이동 시에 새로운 HTML을 받아와야 합니다. 반면, next/link 컴포넌트를 사용하면 링크가 생성된 페이지 정보를 사전에 가져와 JavaScript 파일로 미리 로드하게 됩니다. 이를 통해 페이지 이동 전에 필요한 데이터를 사전에 가져와 클라이언트 측에서 CSR과 유사한 방식으로 처리할 수 있습니다. 또한, next/link는 프리렌더링을 통해 서버에서 HTML을 생성하므로 SEO 측면에서도 문제가 발생하지 않습니다.

### Props

#### href(필수)

이동할 경로나 URL을 지정합니다.

```javascript
import Link from "next/link";

// <Link href="/링크경로">링크이름</Link>;
<Link href="/section1/getStaticProps">/getStaticProps</Link>;
```

![image-20230713231356303](https://raw.githubusercontent.com/ddullgi/image_sever/master/img/image-20230713231356303.png)

렌더링 후 element 상에서는 `<a>`태그로서 동작한다.

#### replace(default: false)

현재의 기록 상태(history state)를 대체하여 새로운 URL을 브라우저 기록 스택에 추가해줍니다.

- 활용 예시

게시글을 읽기 위해 리캡챠나 로그인과 같은 인증 절차가 필요한 사이트의 경우, 사용자가 게시글을 읽은 후에 게시판 목록으로 돌아가려는 경우가 종종 있습니다. 그러나 기존의 방식으로는 이미 완료한 인증 절차를 다시 거쳐야 하고, 다시 한 번 뒤로가기 버튼을 클릭해야 하는 번거로움이 생길 수 있습니다. 이러한 상황에서 replace 속성을 활용하면, 사용자가 게시글 페이지에서 뒤로가기 버튼을 클릭할 때, 이미 수행한 인증 페이지로 되돌아가지 않고 바로 게시판 목록 페이지로 이동할 수 있습니다. 이로써 사용자의 경험을 개선하고 의도한 작업을 보다 원활하게 수행할 수 있게 됩니다.

#### prefetch(default: true)

백그라운드에서 페이지(주소로 표시되는 페이지)를 프리로딩합니다.뷰포트 안에 있는 모든 <Link />는 프리로드되며 뷰포트 바깥에 있을 경우 스크롤을 통해 <Link />가 뷰포트 내에 들어온 순간 프리로드 됩니다. prefetch는 프로덕션 환경에서만 활성화 되고 개발환경에서는 동작하지 않습니다.

- 예시

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

#### scroll(default: true)

<Link>가 새 경로로 이동할 때 페이지의 맨 위로 스크롤해줍니다. 뒤로/앞으로 탐색하는 경우에는 이전의 스크롤 위치를 유지해 줍니다. false로 할 경우 <Link>가 페이지 이동 후 페이지 맨 위로 스크롤하지 않습니다.

## next/router

> [next/link](#nextlink)의 내용 참고

`next/router`는 Next.js에서 제공하는 라우팅 관련 기능을 사용할 수 있는 모듈입니다. `next/link`와 유사한 역할을 하며, 클라이언트 사이드에서의 라우팅을 지원합니다. 그러나 `next/link`와 달리 프리로딩 기능을 제공하지는 않습니다.

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

### useRouter 메서드

- router.push: 지정한 경로로 클라이언트 사이드 네비게이션을 수행하며, 히스토리 스택에 기록합니다.
- router.replace: 경로가 이동되며, 현재의 히스토리 스택을 이동한 경로로 교체합니다.
- router.refresh: 현재 경로를 새로고침합니다. 서버에 새로 요청을 보내 데이터를 리패치하고 서버 컴포넌트를 리렌더링합니다. 클라이언트는 업데이트 된 서버 컴포넌트 데이터를 받아와서 클라이언트의 리액트 상태(ex: useState)나 브라우저의 상태(ex: 스크롤 위치)를 초기화 하지 않고 업데이트합니다.
- router.back: 히스토리 스택에서 이전 경로로 이동합니다.
- router.forward: 히스토리 스택에서 다음 경로로 이동합니다.

## next/image
