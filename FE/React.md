# React

- [가상 DOM](#가상-dom)

<br>

## 가상 DOM

`가상 DOM`은 View에 변화가 있는 경우 현재 `가상 DOM`과 새로운 `가상 DOM`을 비교하여 변경된 내용만 한번에 DOM으로 전달 시켜주는 역할을 합니다. 예를 들어 10개의 노드가 수정될 경우 10번의 레이아웃 계산과 10번의 리렌더링을 초래합니다. `가상 DOM`은 이러한 변화를 DOM에 바로 전달하지 않고 이전 `가상 DOM`과 달라진 부분을 한번만 DOM에 전달하여 한번의 리렌더링만 일어나게 하는 역할을 합니다.

사실 위에서 설명한 역할은 `가상 DOM`뿐만이 아니라 `DOM fragment`도 가능합니다. 하지만 `DOM fragment`경우 해당 과정을 개발자가 수동으로 하나하나 해줘야 됩니다. `가상 DOM`은 이 과정을 자동으로 수행한다는 장점을 가지고 있습니다.
