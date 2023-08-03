# App Router

- [App Router](#app-router-1)
- [Pages](#pages)

<br>

## App Router

Next.js 13 버전에서는 React Server Components를 기반으로 한 새로운 App Router가 도입되었습니다. 이 App Router는 공유 레이아웃, 중첩 라우팅, 로딩 상태 처리, 에러 처리 등 다양한 기능을 지원합니다.

App Router는 "app"이라는 새 디렉토리에서만 작동합니다. 이 새 디렉토리는 기존의 "pages" 디렉토리와 함께 사용되며, 점진적으로 App Router로 바뀔 수 있도록 복수 지원합니다. 이를 통해 기존의 "pages" 디렉토리를 사용하던 기능과 함께 새로운 App Router를 사용하는 기능을 혼용할 수 있습니다. 다만, 두 가지 라우팅 방식이 같은 경로를 가지고 있다면 충돌을 방지하기 위해 빌드 타임에 App Router이 Pages Router보다 우선적용됩니다.

<br>

### 파일 기반 라우트

Next.js는 파일 시스템 기반의 라우터를 사용합니다. 이때 폴더는 라우트를 정의하는 데 사용됩니다.

![route](https://nextjs.org/_next/image?url=%2Fdocs%2Flight%2Froute-segments-to-path-segments.png&w=1920&q=75&dpl=dpl_3guogY6YECQnnD8P1bp8UJe7CDCH)

각 폴더는 URL segment 에 매핑되는 라우트 segment 를 나타냅니다.

<br>

### 파일 컨벤션

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

<br>

### 컴포넌트 계층구조

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

<br>

## Pages

페이지는 특정 URL 경로에 대한 화면을 담당하는 컴포넌트입니다. 각각의 라우트는 자신만의 페이지를 가지며, 이를 통해 각 라우트 폴더에 page.js 파일로 고유한 UI를 정의할 수 있습니다. 이렇게 정의된 페이지는 해당 라우트에 접속했을 때 화면에 표시됩니다. 이를 통해 다양한 페이지를 만들고 라우트별로 다른 UI를 제공할 수 있게 됩니다.

![pages](https://nextjs.org/_next/image?url=%2Fdocs%2Flight%2Fpage-special-file.png&w=1920&q=75&dpl=dpl_BfrsMtEkFNtWCS4n2Nhqya4WuovP)

### ex)

```tsx
// `app/page.tsx` is the UI for the `/` URL
export default function Page() {
  return <h1>Hello, Home page!</h1>;
}
```

```tsx
// `app/dashboard/page.tsx` is the UI for the `/dashboard` URL
export default function Page() {
  return <h1>Hello, Dashboard Page!</h1>;
}
```

> #### 알아두면 좋은 점
>
> - page 는 항상 라우트 서브트리의 맨 마지막에 위치합니다.
> - `.js`, `.jsx` 또는 `.tsx` 파일 확장자를 사용하여 페이지를 정의할 수 있습니다.
> - 라우트 segment를 공개적으로 접근 가능하게 하려면 page.js 파일이 필요합니다.
> - 기본적으로 페이지는 서버 컴포넌트이지만, 클라이언트 컴포넌트로도 설정할 수도 있습니다.

## Layouts

## Templates

## 라우트 그룹

## 동적 라우트
