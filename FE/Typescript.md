# Typescript

- [제네릭](#제네릭)

<br>

## 제네릭

제네릭이란 타입을 마치 함수의 파라미터처럼 사용하는 것을 의미합니다.

제네릭을 사용하면 함수나 클래스 내에서 사용되는 데이터의 타입을 동적으로 지정할 수 있습니다. 이는 컴파일 시점에 타입을 체크하고 에러를 사전에 발견할 수 있어 런타임 에러를 방지하는 데 도움이 됩니다.

제네릭을 사용하는 가장 간단한 예제로는 배열의 타입 안정성을 보장하는 Array<T>를 들 수 있습니다. T는 타입 매개변수로, 배열에 저장될 요소의 타입을 동적으로 지정할 수 있게 합니다. 예를 들어, Array<number>는 숫자로 이루어진 배열을 의미하며, Array<string>은 문자열로 이루어진 배열을 의미합니다.

```typescript
function logText<T>(text: T): T {
  return text;
}

const str = logText<string>("abc");
const num = logText<number>(1);
```

인터페이스에 제네릭을 선언하는 방법

```typescript
interface Dropdown<T> {
  value: T;
  selected: boolean;
}
```

복수의 타입이 혼합된 제네릭을 선언하는 방법

```typescript
interface Dropdown<T, U> {
  value: T;
  selected: U;
}
```

#### 제네릭의 타입 제한

제네릭을 사용할 경우 동적으로 타입을 정의 할 수 있지만 그로 인해 오류가 발생할 수도 있습니다.

```typescript
function logText<T>(text: T): T {
  console.log(text.length); // Error: T doesn't have .length
  return text;
}
```

위 코드를 보면 선언한 `T`가 어떤 타입인지 구체적인 정의가 없기 때문에 `length` 코드에서 오류가 나게 됩니다. 이럴 경우 `extends`키워드를 사용하여 `length`에 대해 동작하는 인자만 넘겨받을 수 있습니다. 이러한 방식을 제네릭의 타입 제한이라고 합니다.

```typescript
interface LengthType {
  length: number;
}

function logTextLength<T extends LengthType>(text: T): T {
  console.log(text.length);
  return text;
}

logTextLength("text");
logTextLength({ length: 0, value: "hi" }); // `text.length` 코드는 객체의 속성 접근과 같이 동작하므로 오류 없음
logTextLength(true); // 'boolean' 형식의 인수는 'LengthType' 형식의 매개 변수에 할당될 수 없습니다.ts(2345)
```
