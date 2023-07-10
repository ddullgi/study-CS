# JAVASCRIPT

- [scope](#scope)
- [AJAX](#AJAX)

<br>

## scope

모든 식별자(변수, 이름, 함수 이름, 클래스 이름 등)는 자신이 선언된 위치에 의해 참조되는 유효 범위가 결정 된다. 이를 **scope**라고 한다. 즉, 식별자의 유효한 범위를 말한다.

**종류**

- 전역 scope: 코드의 가장 바깥 영역
- 지역 scope: 함수나 블록의 안쪽 영역 (지역 변수는 자신의 지역 scope와 그 하위에서만 유효함)

**scope 체인**

변수를 참조할 때 자바스크립트 엔진은 scope 체인을 통해 변수를 참조하는 코드의 scope에서 시작하여 상위 scope 방향으로 이동하며 선언된 변수를 검색한다.

**scope의 레벨**

- 함수 레벨 scope: var 변수의 경우 블록 레벨의 scope를 무시하고 함수 단위에서만 scope를 만듬
- 블록 레벨 scope: const, let 변수에 경우 함수 레벨 뿐만 아니라 블록 레벨(if, for문 등) 단위에서 적용되는 scope를 만듬

<br>

## AJAX

`Asynchronous JavaScript And XML`은 서버로부터 웹페이지의 변경에 필요한 데이터만 비동기 방식으로 전송 받아 웹페이지를 변경할 필요가 없는 부분은 다시 렌더링하지 않고, 변경할 필요가 있는 부분만 한정적으로 렌더링하는 방식을 말합니다.

![image-20230711051603457](https://raw.githubusercontent.com/ddullgi/image_sever/master/img/image-20230711051603457.png)

> **XMLHttpRequest**
>
> 서버와 상호작용하기 위해 사용되며 전체 페이지의 새로 고침 없이 데이터를 받아 올 수 있는 자바스크립트의 객체입니다. 이름과 달리 XML뿐만 아니라 모든 종류의 데이터를 받아올 수 있습니다.
