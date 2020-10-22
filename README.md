# JavaScript TIL

> 기본적으로 **[모던 자바스크립트 Deep Dive](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&linkClass=331405&barcode=9791158392239)**책을 기반으로 학습하며, 유튜브와 구글링을 통해 자료를 추가하였다.



## 1021

- print( 문서에 출력하기 - browser only)

  ```javascript
  document.write('문자열')
  ```

- User input ( 사용자 입력 받기 - browser only)

  ```javascript
  const UserName = prompt('who are you?')
  ```





### 스코프

> 어떤 변수들에 접근할 수 있는지를 정의한다.

​	**1) 전역 스코프(Global Scope)**

​	변수가 함수 바깥이나 중괄호(`{}`) 바깥에서 선언됐으면, 전역 스코프에 정의된다. *전역 변수는 코드 어디서든	지 사용가능하다.*  변수 이름의 중복을 유의하자

​	**2) 지역 스코프(Local Scope)**

​	특정 부분에서만 사용할 수 있는 변수.

​		2-1) 함수 스코프 (Function Scope)

​		함수 내부에서 변수를 선언하면, 그 변수는 선언한 함수 내부에서만 접근 가능하다. 함수 바깥에서 접근 불가.

​		2-2) 블록 스코프 (Block Scope)

​		중괄호 내부에서 변수를 선언하면, 그 변수들은 중괄호 블록 내부에서만 접근할 수 있다.

​		*함수를 선언할 때에는 중괄호를 사용해야 하므로, 블록 스코프는 함수 스코프의 서브셋이다.*



- 함수는 서로의 스코프에 접근할 수 없다.

- **네스팅된 스코프 ( Nested Scope) ** : 함수 안에 다른 함수가 내부에서 정의되었다면, 내부 함수는 외부 함수의 변수에 접근할 수 있다. 이런 행동을 렉시컬 스코핑(lexical scoping)이라고 부른다. *반면, 외부 함수는 내부 함수의 변수에 접근할 수 없다.*



#### 클로저 (Closures)

> 함수 내부에 **함수를 작성할 때 마다 내부에 작성된 함수** 즉, 클로져가 생성된다. 클로저는 외부 함수의 변수를 사용할 수 있기 때문에 대개 반환하여 사용한다.

- 클로저의 대표적인 두 가지 목적
  - 사이드 이펙트 (side effect ) 제어
    - 함수에서 값을 반환하는 것을 제외하고 무언가를 행할 때 사이드 이펙트가 발생한다. `Ajax`요청이나 `timeout`, 그리고 `console.log` 선언 등 모두 사이드 이펙트가 된다. 이를 클로져를 통해 사이드 이펙트를 제어한다.
  - private  변수 생성
    - 함수 내부의 변수는 함수 바깥에서 접근할 수 없어서 `private 변수`라고 불린다. 하지만, 해당 변수들에 접근해야 할 경우가 있는데, 이를 클로저를 통해서 접근할 수 있다.

<hr>
- Object Literal +

  object의 key와 value가 똑같다면, 마치 배열처럼 한 번만 작성 가능

  ex)

  ```javascript
  let books = array...;
  let comics = object...;
  let magazines = null;
  
  const bookShop={
      books,
      comics,
      magazines,
  };
  ```

  

- JSON은 실제로 Object 처럼 사용하려면 다른 언어들 처럼 Parsing(구문 분석) 작업이 필요하다.
  - **object => JSON** : JSON.stringify(Object)  / typeof로 확인하면 string
  - **JSON => object** : JSON.parse(JSON) / typeof로 확인하면 object



## 1022 JS의 특징, 변수

- `자바스크립트는` 프로그래밍 언어로서의 기본 뼈대를 이루는 `ECMASCript`와 브라우저가 별도 지원하는 `클라이언트 사이드 Web API`등을 아우르는 개념이다.
  - `클라이언트 사이드 Web API` : DOM, BOM, Canvas, XMLHttpRequest, fetch, requestAnimationFrame, SVG, Web Storage, Web Component, Web Worker 등



- 자바스크립트는 명령형(imperative), 함수형(functional), 프로토타입 기반 (prototype-based) 객체지향 프로그래밍을 지원하는 멀티 패러다임 프로그래밍 언어이다.



- 자바스크립트는 별도의 컴파일 작업을 수행하지 않는 `인터프리터 언어(interpreter language)`이다. 대부분의 모던 자바스크립트 엔진은 인터프리터와 컴파일러의 장점을 결합해 비교적 처리 속도가 느린 인터프리터의 단점의 해결했다. 

  -> 전통적인 컴파일 언어 처럼 명시적인 컴파일 단계를 거치지는 않지만 복잡한 과정을 거치며 일부 소스코드를 컴파일하고 실항한다.



- 