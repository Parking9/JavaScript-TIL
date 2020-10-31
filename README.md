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
>
> 식별자가 유효한 범위를 말함. (식별자를 검색하는 규칙!)

​	**1) 전역 스코프(Global Scope)**

​	변수가 함수 바깥이나 중괄호(`{}`) 바깥에서 선언됐으면, 전역 스코프에 정의된다. *전역 변수는 코드 어디서든	지 사용가능하다.*  변수 이름의 중복을 유의하자



​	전역변수를 반드시 사용해야 할 이유를 찾지 못한다면 지역변수를 사용해야한다. **변수의 스코프는 좁을수록 		좋다,**

​	그 이유는 1) 모든 코드가 전역변수를 참조하고 변경할 수 있는 암묵적 결합을 허용한다. 2) 전역 변수는 생명 주	기가 길다. 3) 스코프 체인 상에서 종점에 존재한다. ( 전역 변수의 검색속도가 가장 느리다.) 4) 파일이 분리되어	있다 해도 전역 스코프를 공유한다.

​	

​	**<전역 변수의 사용을 억제하는 방법>**

​	1) 즉시 실행 함수 : 모든 코드를 즉시 실행 함수로 감싸면 모든 변수는 즉시 실행 함수의 지역변수가 된다.

​	2) 네임스페이스 객체 : 네임스페이스 역할을 담당할 객체를 생성하고 전역 변수처럼 사용하고 싶은 변수를 프로	퍼티로 추가한다. 이 방법은 식별자 충돌을 방지 하지만, 객체가 전역 변수이므로 유용하지는 않다고 본다.

​	3) 모듈 패턴 : 전역변수의 억제 + 캡슐화 가능.



​	**2) 지역 스코프(Local Scope)**

​	특정 부분에서만 사용할 수 있는 변수.

​	지역변수의 생명주기는 함수의 생명 주기와 일치한다.



​		2-1) 함수 스코프 (Function Scope)

​		함수 내부에서 변수를 선언하면, 그 변수는 선언한 함수 내부에서만 접근 가능하다. 함수 바깥에서 접근 불가.

​		2-2) 블록 스코프 (Block Scope)

​		중괄호 내부에서 변수를 선언하면, 그 변수들은 중괄호 블록 내부에서만 접근할 수 있다.

​		*함수를 선언할 때에는 중괄호를 사용해야 하므로, 블록 스코프는 함수 스코프의 서브셋이다.*

​		ES6에서 도입된 let, const 키워드는 블록 레벨 스코프를 지원한다. 



- 함수는 서로의 스코프에 접근할 수 없다.
- **네스팅된 스코프 ( Nested Scope) ** : 함수 안에 다른 함수가 내부에서 정의되었다면 (= 스코프가 함수의 중첩에 의해 계층적 구조를 갖는다면), 내부 함수는 외부 함수의 변수에 접근할 수 있다. 이런 행동을 렉시컬 스코핑(lexical scoping)이라고 부른다. *반면, 외부 함수는 내부 함수의 변수에 접근할 수 없다.*
- 스코프가 계층적으로 연결된 것을 스코프체인(scope chain)이라 한다. 자바스크립트 엔진은 변수를 참조할 때 스코프체인을 통해 변수를 참조하는 코드의 스코프에서 시작하여 상위 스코프 방향으로 이동하며 선언된 변수를 검색한다.







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



### 변수(Variavle)

>하나의 값을 저장하기 위해 확보한 메모리 공간 자체  또는 그 메모리 공간을 식별하기 위해 붙인 이름을 말한다. 
>
>프로그래밍 언어에서 값을 저장하고 참조하는 메커니즘으로, **값의 위치를 가리키는 상징적인 이름을 말한다.**



- 컴퓨터는 메모리를 사용해 데이터를 기억한다. 메모리는 데이터를 저장할 수 있는 메모리 셀의 집합체로 메모리 셀 하나의 크기는 1바이트(8비트)이다. 즉 1 바이트 단위로 데이터를 저장하거나 읽어들인다. 각 셀은 고유의 메모리 주소를 갖고, 이 메모리 주소는 메모리 공간의 위치를 말한다. 컴퓨터는 모든 데이터를 2진수로 처리하는데 메모리에 저장되는 데이터는 데이터의 종류(숫자, 텍스트, 이미지, 동영상 등)와 상관없이 모두 2진수로 저장된다. 



- 데이터를 읽어오기 위하여 데이터가 저장된 메모리 공간에 직접 접근하는것은 치명적인 오류를 발생시킬 가능성이 높은 매우 위험한 일이다. 따라서 프로그래밍 언어의 컴파일러 또는 인터프리터에 의해 *값이 저장된 메모리 공간의 주소로 치환된 변수가 실행된다.*



- 새로운 데이터가 메모리 공간에 저장되고, 이 데이터를 다시 읽어 들여 재사용할 수 있도록 저장된 메모리 공간에 상징적인 이름을 붙인것이 바로 변수이다.
- 변수에 값을 저장하는 것을 할당 (assignment, 대입, 저장)이라고 하고, 변수에 저장된 값을 읽어 들이는 것을 참조 (reference)라고 한다. 



- 변수의 이름을 식별자(identifier)라고도 한다. 식별자는 어떤 값을 구별해서 식별할 수 있는 고유한 이름을 말한다. 값은 메모리 공간에 저장되어 있는데, 식별자는 메모리 공간에 저장되어 있는 어떤 값을 구별해서 식별해낼 수 있어야한다. 이를 위해 식별자는 어떤 값이 저장되어 있는 메모리 주소를 기억(저장)해야 한다. --> 식별자는 값이 아니라 메모리 주소를 기억하고 있다. 
- 식별자로 값을 구별해서 식별한다는 것은 식별자가 기억하고 있는 메모리 주소를 통해 메모리 공간에 저장된 값에 접근할 수 있다는 의미이다.



- **변수 선언**은  변수를 생성하는 것을 말한다. 값을 저장하기 위한 메모리 공간을 확보하고 변수 이름과 확보된 메모리 공간의 주소를 연결해서 값을 저장할 수 있게 준비하는 것이다. 선언 `키워드`는 var, let , const이다.
  - `키워드`는 자바스크립트 코드를 해석하고 실행하는 JS엔진이 수행할 동작을 규정한 일종의 명령어다.
  - 변수를 선언만 하고 값을 할당하지 않으면 메모리 공간이 비어있어야하지만, 자바스크립트의 독특한 특징으로 `undefined`라는 값이 암묵적으로 할당되어 초기화 된다.



#### 변수 호이스팅

```javascript
console.log(score) //undefined

var score //변수 선언문
```

위 코드를 보면 변수 선언문보다 변수 참조 코드가 앞에 있다. 따라서 인터프리터에 의해 한 줄씩 순차적으로 실행되므로 참조 에러(Reference Error)가 발생할 것처럼 보인다. 하지만 참조 에러가 발생하지 않고 undefined가 출력된다. **그 이유는 변수 선언이 소스코드가 한 줄씩 순차적으로 실행되는 시점, 즉 런타임이 아니라 그 이전 단계에서 먼저 실행되기 때문이다.**



JS엔진은 인터프리터를 실행하기 전 소스코드의 평가 과정을 거치고 소스코드를 실행하기 위한 준비를 한다. 이 평가 과정에서 변수 선언을 포함한 모든 선언문(변수 선언문, 함수 선언문)을 소스코드에서 찾아내 먼저 실행한다.



이 과정처럼 변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 `변수 호이스팅(Variable Hoisting)`이라한다.



**let**키워드로 선언한 변수는 선언단계와 초기화 단계가 분리되어 진행되어 일시적인 사각지대를 일으킨다. 



- 변수 선언은 소스코드가 순차적으로 실행되는 시점인 런타임 이전에 먼저 실행되지만, 값의 할당은 소스코드가 순차적으로 실행되는 시점인 런타임에 실행된다.



- 변수 재할당은 이미 값이 할당되어 있는 변수에 새로운 값을 또다시 할당하는 것.
  - var 키워드로 사용가능
  - 재할당이 불가한 변수는 `상수`라고 한다. (const 키워드로 사용가능) 선언이 단 한 번.
- 값을 재할당하면 기존의 메모리공간을 사용하는 것이 아니라 새로운 메모리 공간을 확보하고 그 메모리 공간에 저장한다. 이전에 사용한 메모리 공간은 어떠한 식별자와도 연결되어 있지 않고 필요가 없어서 `가비지 콜렉터`에 의해 메모리에서 자동 해체된다.
  - **가비지 콜렉터**는 할당한 메모리 공간을 주기적으로 검사하여 더 이상 사용되지 않는 메모리를 해제하는 기능을 말한다. 이를 통해 메모리 누수(memory leak)를 방지한다.



- **네이밍 컨벤션(Naming Convention)**을 통해 읽기 좋은 의미있는 이름을 사용한다.
  - 변수나 함수 : 카멜 케이스
  - 생성자 함수, 클래서 : 파스칼 케이스



## 1023 타입

- C나 자바의 경우, 정수와 실수를 구분해서 int, float, double 등과 같은 다양한 숫자 타입을 제공한다. 하지만 자바스크립트는 독특하게 하나의 숫자 타입만 존재한다. 이 숫자 타입은 64비트 부동소수점 형식을 따른다. **즉, 모든 수를 실수로 처리하며, 정수만 표현하기 위한 데이터 타입이 별도로 존재하지 않는다.**



- 숫자 타입은 추가적으로 세 자기 특별한 값도 표현할 수 있다. `Infinity`, `-Infinity`, `NaN`



- 일반 문자열 내에서 줄바꿈 등의 공백을 표현하려면 백슬래시로 시작하는 `이스케이프 시퀀스`를 사용해야한다.
- 일반 문자열과 달리 `템플릿 리터럴` 내에서는 이스케이프 시퀀스를 사용하지 않고도 줄바꿈이 허용되며, 모든 공백도 있는 그대로 적용된다.



- **문자열에 표현식을 삽입하려면 반드시 템플릿 리터럴을 사용해야하고**, `${}`으로 표현식을 감싼다. 표현식의 평가 결과가 문자열이 아니더라도 문자열로 타입이 강제로 변환되어 삽입된다.



- undefined는 개발자가 의도적으로 할당하기 위한 값이 아니라 자바스크립트 엔진이 변수를 초기화할 떄 사용하는 값이다. 변수에 값이 없다는 것을 명시하고 싶을 때는 null을 할당한다.
- 







## 1029

- let, const
- 블록 레벨 스코프





## 1030

- 프로퍼티 어트리뷰트
- 생성자 함수에 의한 객체 생성



## 1031 

- 객체지향 프로그램
- 프로토타입
- 함수와 일급객체