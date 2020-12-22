# JavaScript TIL

> 기본적으로 **[모던 자바스크립트 Deep Dive](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&linkClass=331405&barcode=9791158392239)**책과 함수형 프로그래밍과 JavaScript ES6+ 강의를 중심으로 학습하며, 유튜브와 구글링을 통해 자료를 추가하였다.



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



**자바스크립트는 함수를 어디서 호출했는지가 아니라 어디에 정의했는지에 따라 상위 스코프를 결정한다.**



​	**1) 전역 스코프(Global Scope)**

​	변수가 함수 바깥이나 중괄호(`{}`) 바깥에서 선언됐으면, 전역 스코프에 정의된다. *전역 변수는 코드 어디서든	지 사용가능하다.*  변수 이름의 중복을 유의하자



​	전역변수를 반드시 사용해야 할 이유를 찾지 못한다면 지역변수를 사용해야한다. **변수의 스코프는 좁을수록 좋다,**

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

**외부 함수보다 중첩 함수가 더 오래 유지되는 경우 중첩함수는 이미 생명주기가 종료한 외부 함수의 변수를 참조할 수 있다. 이러한 중첩 함수를 클로저라고 한다.**

*외부 함수의 실행 컨텍스트가 실행 컨텍스트 스택에서 제거되지만 외부함수의 렉시컬 환경까지 소멸하는 것은 아니다*  **가비지 콜렉터는 누군가 참조하는 메모리 공간을 함부로 해제하지 않는다.**

외부 함수를 참조하지 않는 경우는 최적화를 통해 상위 스코프를 기억하지 않는다. 

또한, 외부 함수보다 먼저 소멸되면 클로저의 본질에 부합하지 않는다.



**클로저에 의해 참조되는 상위 스코프의 변수를 자유변수(free variable)이라고 한다. 클로저의 의미는 함수가 자유변수에 대해 닫혀있다는 의미이다. ( 자유변수에 묶여있는 함수)**




- 클로저의 대표적인 두 가지 목적
  - 사이드 이펙트 (side effect ) 제어
    - 함수에서 값을 반환하는 것을 제외하고 무언가를 행할 때 사이드 이펙트가 발생한다. `Ajax`요청이나 `timeout`, 그리고 `console.log` 선언 등 모두 사이드 이펙트가 된다. 이를 클로져를 통해 사이드 이펙트를 제어한다.
  - private  변수 생성
    - 함수 내부의 변수는 함수 바깥에서 접근할 수 없어서 `private 변수`라고 불린다. 하지만, 해당 변수들에 접근해야 할 경우가 있는데, 이를 클로저를 통해서 접근할 수 있다.

--> 상태변경이나 가변 데이터를 피하고 불변성을 지향하는 함수형 프로그래밍에서 부수효과를 최대한 억제하여 오류를 피하고 안정성을 높이기 위해 클로저가 적극적으로 사용된다.



- 캡슐화(capsulation)는 객체의 상태를 나타내는 프로퍼티와 프로퍼티를 참조하고 조작할 수 있는 동작인 메서드를 하나로 묶는 것을 말한다.
- 캡슐화는 객체의 특정 프로퍼티나 메서드를 감출 목적으로 사용하기도 하는데 이를 정보 은닉이라 한다.
- 정보은닉을 통해 적절치 못한 접근으로부터 객체의상태가 변경되는 것을 방지해 정보를 보호하고, 객체 간의 상호 의존성, 즉 결합도(coupling)를 낮출 수 있다.



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



### 가비지 콜랙터

객체를 포함한 모든 값은 누군가에 의해 참조되지 않을 떄 비로소 가비지 컬렉터에 의해 메모리 공간의 확보가 해제되어 소멸한다.





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

**전역 환경 레코드를 생성하며 전역 코드 평가 시점에 전역 객체에 변수 식별자를 키로, 값을 undefined로 암묵적으로 바인딩한다.  따라서, 코드 실행 단계에서 변수 선언문 이전에도 참조할 수 있다. 이것이 호이스팅 (변수, 함수)이 발생하는 원인이다.**



> 변수에 선언한 함수 표현식도 호이스팅 되는데 이를 함수 호이스팅이라고 한다.

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



## 1102

- 프로토타입 체인
- 오버라이딩, 프로퍼티 섀도잉
- 프로토타입의 교체
- instanceof
- 직접 상속
- 정적 프로퍼티/메서드

- 프로퍼티 존재 확인 (in, Reflect.has(),hasOwnProperty)
- 프로퍼티 열거 (for ... in , forEach, for ... of   // keys(), values(), entries() )





- strict mode     암묵적 전역(implicit global)



- built-in 객체
- 원시값과 래퍼객체
- 전역객체   (browser, Node.js)
  - 빌트인 전역 프로퍼티 : Infinity, NaN, undefined
  - 빌트인 전역 함수 : eval, isFinite, inNaN, parseFloat, parseInt (+toString), encodeURI & decodeURI, encodeURLComponent & decodeURIComponent, 



- this
  - **this 동적 바인딩** (`일반 함수` --> 명시적 바인딩, `메서드 바인딩` --> 메서드를 호출한 객체)
  - `생성자 함수 호출` (함수가 생성할 인스턴스,   new 연산자와 같이 호출하지 않으면 일반 함수)
  - `Function prototype`의 apply(array), call(..,..,..,..) --> 호출할 함수에 인수를 전달하여 호출 함수 실행, bind(인자)() --> 명시적 호출이 필요함



- 실행 컨텍스트
  - 4가지 타입의 소스코드. 타입에 따라 실행 컨텍스트 생성 과정과 관리 내용이 다르다. >> 전역 코드 , 함수 코드, eval 코드, 모듈 코드 
  - 소스코드의 평가와 실행
  - 1. 전역 코드의 평가  2. 전역 코드 실행 3. 함수 코드 평가 4. 함수 코드 실행 >> 스코프를 구분하여 식별자와 바인딩된 값을 관리 & 스코프체인으로 식별자 검색, 전역 객체의 프로퍼티도 전역 변수처럼 검색
  - 실행 컨텍스트의 역할 : 스코프, 식별자, 코드 실행 순서 등의 관리
  - 실행 컨텍스트는 스택 자료구조로 관리됨. **실행 컨텍스트 스택**
  - **렉시컬 환경**은 `식별자와` 바인딩된 값, 상위 `스코프`에 대한 참조를 기록하는 자료구조로 실행 컨텍스트를 구성하는 컴포넌트다. 1) 식별자와 바인딩된 값을 관리하는 저장소인 환경 레코드와 2) 스코프 체인을 구현하는 외부 렉시컬 환경에 대한 참조  두 개의 컴포넌트로 구성된다.
  - **실행 컨텍스트의 생성과 식별자 검색 과정**
    - 전역객체 생성 (코드평가 이전)
    
    - 전역 코드 평가
      - 전역 실행 컨텍스트 생성
      - 전역 렉시컬 환경 생성
        - 전역 환경 레코드 생성 (객체 환경 레코드, 선언적 환경 레코드)
      - 전역 환경 레코드 생성
      - this 바인딩
      - 외부 렉시컬 환경에 대한 참조 결정
      
    - 전역 코드 실행 (식별자 결정--> 스코프체인)
    
    - foo함수 코드 평가 (foo 함수 내부로 코드 제어권 이동하여 함수 코드 평가)
    
    - foo함수 실행 및 종료
    
    - 전역 코드 실행 종료
    



## 1217

<b> 일급</b>

- 값으로 다룰 수 있다.
- 변수에 담을 수 있다.
- 함수의 인자로 사용될 수 있다.
- 함수의 결과로 사용될 수 있다.



<b> 일급함수</b>

- 함수를 값으로 다룰 수 있다.
- 조합성과 추상화의 도구

```javascript
const add5 = a => a+5  #변수에 함수를 값으로 담을 수 있다.
log(add5) a => a+5
log(add5(10)) 15  #결과를 다른 함수에 전달

const f1 = () => () => 1 
log(f1()) () => 1 #함수를 인자로 담을 수 있다.

const f2 = f1()
log(f2) () => 1
log(f2()) 1 
```



<b>고차함수</b>

일급함수라는 특징을 사용하여 함수를 값으로 받아서 사용하는 함수

- 함수를 인자로 받아서 실행하는 함수

  ```javascript
  const apply1 = f => f(1);
  const add2 = a => a+2 
  log(apply1(add2)) 3
  ```

  ```javascript
  const times = (f,n) => {
      let i = -1
      while(++i < n) f(i)
  };
  
  times(log,3) 0 1 2
  times(a=> log(a+10), 3) 10 11 12
  # 함수를 인자로 받아서 원하는 인자를 받아서 함수를 실행
  ```



- 함수를 만들어서 리턴하는 함수(클로저를 만들어서 리턴하는 함수)

  ```javascript
  const addMaker = a => b => a+b; #클로저를 리턴하는 함수
  const add10 = addMaker(10);
  log(add10); b=> a+b
  log(add10(5)); 15
  log(add10(10)); 20
  ```

  

<b>리스트 순회</b>

```javascript
const list = [1,2,3];
for (const a of list){
    log(a);
}
1 2 3

const str = 'abc';
for (const a of str){
    log(a);
}
a b c
```



## 1218

- <b>이터러블/이터레이터 프로토콜</b>
  - 이터러블 : 이터레이터를 리턴하는 `[Symbol.iterator]()`를 가진 값
  - 이터레이터 : {value, done} 객체를 리턴하는 next()를 가진 값
  - 이터러블/이터레이터 프로토콜 : 이터러블을 for... of, 전개 연산자 등과 함께 동작하도록한 규약

 

```javascript
# Array
const arr = [1,2,3];
let iter = arr[Symbol.iterator]();
for (const a of iter) log(a) # arr는 이터레이터를 순회하면서 안쪽에 value를 출력해줌


# Set
const set = new Set([1,2,3]);
for (const a of set) log(a); #


# Map
const map = new Map(['a',1], ['b',2], ['c',3]);
for (const a of map ) log(a); 

# map.keys() key를 가진 iterator 반환
# map.values() value를 가진 iterator 반환
# map.entries() key,value를 가진 iterator 반환


```



이터레이터의 Symbol.iterator가 자기 자신일 경우에 well formed iterable, iterator라 할 수 있다.

iterator 또한 iterable로 만들어야 한다.

```javascript
const arr = [1,2,3];
let iter2 = arr[Symbol.iterator]();

log(iter2[Symbol.iterator]() == iter2) #true;
```



사용자 정의 iterable

```javascript
const iterable = {
	[Symbol.iterator]() {
        let i = 3;
        return {
            next() {
                return i==0 ? {done : true} : {value : i--, done : false};
            },
            [Symbol.iterator]() {return this;}
        }
    }
}
```



- <b>전개 연산자</b>

전개 연산자 또한 이터러블/이터레이터 포로토콜을 따른다.

```javascript
const a = [1,2,3]
log([...a, ...[3,4,5]]) #[1,2,3,3,4,5]

const b=[1,2,3]
b[Symbol.iterator] = null
log([...b, [3,4,5]]) #TypeError : b is not iterable
```



- <b>제너레이터/이터레이터</b>

>  제너레이터 : 이터레이터이자 이터러블을 리턴하는 함수

```javascript
function *gen(){
    yield 1;
    yield 2;
    yield 3;
    return 100; # 마지막 done : true일때 나오는 값
}

let iter = gen()
log(iter[Symbol.iterator]); # f [Symbol.iterator]() well-formed iterator를 리턴하는 함수이다. 
log(iter[Symbol.iterator]() === iter ) # true
log(iter.next()) # {value : 1, done : false}
log(iter.next()) # {value : 2, done : false}
log(iter.next()) # {value : 3, done : false}
log(iter.next()) # {value : 100, done : true}

for (const a of gen()) log(a) # 1 2 3 (return은 나오지 않음)

제너레이터는 순회할 값을 문장으로 표현함.
JS에서는 어떠한 값이든 제너레이터면 순회할 수 있다.

function *gen(){
    yield 1;
    if (false) yield 2;
    yield 3;
    return 100; # 마지막 done : true일때 나오는 값
}
for (const a of gen()) log(a) # 1 3

어떠한 값도 순회할 수 있는 형태로 만들 수 있다. 
```



<b>제너레이터를 활용해 odd만 담고있는 iterator 생성 </b>

```javascript
function *odds(n) {
    for (let i = 0; i < n; i++){
        if (i%2) yield i;
    }
}
let iter = odds(10)

# 최대 10인 홀수만 뽑는 iterator 생성됨.
```

``` javascript
# 제너레이터를 활용해

# 무한히 증가하는 iterator 생성
function *infinity(i=0){
    while(true) yield i++
}

# 매개변수로 주어진 iterator를 순회하며 주어진 n까지만 순회하는 iterator 생성
function *limit(n, iter){
    for (const a of iter ){
        yield a;
        if (a ===n ) return
    }
}

# 1부터 n 무한히 증가하는 iterator에서 홀수만 갖는 iterator 생성
function *odds(n){
    for (const a of limit(n, infinity(1))){
        if (a%2) yield a;
	}
}

let iter = odds(40)
for(const a of iter) log(a) #  1 3 5 7 ...  35 37 39
```



제너레이터는 `for of`, `전개 연산자`, `구조 분해`, `나머지 연산자` 등 이터러블/이터레이터 프로토콜을 따르는 라이브러리나, 함수들과 함께 사용될 수 있다.

```javascript
# 전개 연산자
log(...odds(10)) # 1 3 5 7 9
log([...odds(10), ...odds(20)]) # 1 3 5 7 9 1 3 .. 19

# 구조 분해
const [head, ...tail] = odds(5)
log(head) # 1
log(tail) # [3, 5]

# 나머지 연산자
const [a, b, ...rest] = odds(10)
log(a) # 1
log(b) # 3
log(rest) #[5,7,9]
```

제너레이터와 이터레이터를 잘 활용해하여 조합성이 높은 프로그래밍이 가능하다. 



## 1221

- <b>map</b>

> 이터러블 프로토콜을 따르는 map의 다형성

```javascript
const products =[
    {name : '사과', price : 100},
    {name : '바나나', price : 200},
    {name : '포도', price : 300}
]


let names = [];
for ( const p of products){
    names.push(p.name)
}
log(names) # ['사과','바나나','포도']

# 어떠한 iterable도 받을 수 있는 변수와, 어떤 값을 수집할 것인지 함수를 통해 받음(보조함수).
const map = (f,iter)=>{
    let res =[]
    for (const i of iter){
		res.push(f(i));        
    }
    return res;
}
console.log(map(p=>p.name, products)) # ['사과','바나나','포도']

```

```javascript
log(document.querySelectorAll('*').map(el => el.nodeName)) #undefined
document.querySelectorAll('*')는 NodeList이지 array가 아니기 때문에

document.querySelectorAll('*')[Symbol.iterator]() # array iterator

# 이터러블 프로토콜을 따르는 모든 iterable인 모든 값, 제너레이터 등 모두 map을 할 수 있다.
# ex-1
function *gen(){
    yield 2;
    if(false) yield 3;
    yield 4;
}
log(map(a=>a*a, gen())) [4, 16]

#ex-2
let m = new Map()
m.set('a',10)
m.set('b',20)
log(map(([key,value])=>[key,2*value]),m); #[['a',20],['b',40]]

```

<b>이터러블 프토토콜을 따르는 함수들을 사용하는것은 많은 다른 헬퍼 함수들과의 조합이 좋아진다.</b> 



- <b>filter</b>

> 특정 조건으로 iterable한 객체를 필터링함.

```javascript
const products =[
    {name : '사과', price : 100},
    {name : '바나나', price : 200},
    {name : '포도', price : 300}
]

let under200 = []
for ( const p of products){
    if(p.price < 200) under200.push(p)
}
console.log(under200) #{name : '사과', price : 100}


const filter = (f, iter) => {
    let res = []
    for (const a of iter ){
        if (f(a)) res.push
    }
    return res
}

log(filter(p=> p.price < 200, products)) #{name : '사과', price : 100}


# filter 역시 이터러블 프로토콜을 따르고 내부 함수와 이터러블 프로토콜을 따르는 객체를 받아줌으로써 다형성을 높이고 재사용성이 좋음
```



<b>reduce</b>

> 하나의 축약된 값으로 표현

```javascript
const products =[
    {name : '사과', price : 100},
    {name : '바나나', price : 200},
    {name : '포도', price : 300}
]


const nums = [1,2,3,4,5];

let total = 0;
for ( const n of nums ){
    total+=n
}
console.log(total) #15


# reduce의 실행 절차는 다음과 같다
const add = (a, b) => a+b;

console.log(reduce(add,0,[nums])) # 15
# add(add(add(add(add(0,1),2),3),4),5) 재귀적으로 내부함수를 호출하여 하나의 값으로 리턴

const reduce = (f, acc, iter) =>{
    for (const i of iter){
        acc = f(acc,i);
    }
    return acc;
};
console.log(add,0,nums) #15

# 초기값인 acc가 없으면 iter의 첫번째 인자를 초기값으로 만든다.
const reduce = (f,acc,iter)=> {
    if(!iter){
        iter = acc[Symbol.iterator]();
        acc = iter.next().value
    }
    for (const i of iter){
        acc = f(acc,a)
    }
    return acc
}
console.log(add,nums) # 15
```



```javascript
const products =[
    {name : '사과', price : 100},
    {name : '바나나', price : 200},
    {name : '포도', price : 300}
]

console.log(
	reduce(
        (total, product) => total+=product.price,
        0,
        products
    )
); #600

# 보조함수를 통해 안쪽에 있는 값의 다형성을 지원하고, iterable을 통해 외부의 다형성도 지원하는 함수
```



<b>map+filter+reduce</b>

```javascript
const products =[
    {name : '사과', price : 100},
    {name : '바나나', price : 200},
    {name : '포도', price : 300},
    {name : '파인애플', price : 400},
    {name : '체리', price : 500},
]

# 특정 가격 미만의 상품의 가격만 출력
console.log(map(a => a.price, filter(p => p.price < 300, products)));
# [100,200]

# 특정 가격 미만의 상품들의 가격의 합
console.log(
    reduce(
        add,
        map(a => a.price,								 
            filter(p => p.price < 300, products))	
    )
);
# 300

# ***** 코드가 평가될때, 각 매개변수에 알맞은 형태의 데이터로 평가되도록 기대하고 함수들을 사용하여, 코드를 작성해야한다.*****
# 함수형 프로그래밍에서는 이런식으로 사고를 하며 코드를 작성해나간다.
```



<b>함수형 프로그래밍은 `코드를 값으로 다루는 아이디어`를 많이 사용한다. 코드를 값으로 다루기에 어떤 함수가 코드인 함수를 받아서 평가하는 시점을 원하는대로 다룰 수 있다. 이로 코드의 표현력을 높일 수 있다. </b>



- <b>go</b>

```javascript
console.log(
    reduce(
        add,
        map(a => a.price,								 
            filter(p => p.price < 300, products))	
    )
);
# 이러한 코드를 좀 더 단순하게 표현하기 위해 go라는 함수를 만든다.

go(
    0,
    a=> a+1,
    a => a+10,
    a => a+100,
    console.log
)
# 이렇게 연속적으로 함수를 받는 go 함수를 만든다. 인자들을 받아 하나의 값으로 축약 (=reduce)

const go  = (..args) => reduce((a,f)=> f(a), args)
# 111


# 이러한 go 함수를 통해 위의 코드를 아래와 같이 읽기 좋게 표현할 수 있다.
go(
    products,
    products => filter(p=> p.price < 300, products),
    products => map(p=> p.price, products),
    prices => reduce(add, prices),
    console.log
)
#300
```



- <b>pipe</b>

> go와 달리 함수를 리턴하는 함수. 함수들이 나열되어있는 합성된 함수를 만들어내는 함수

```javascript
const f = pipe(
    a => a+1,
    a => a+10,
    a => a+100,
);

const pipe = (...fs) => (a) => go(a, ...fs);

console.log(f(0)); # 111



const f = pipe(
    (a,b) => a+b,
    a => a+10,
    a => a+100,
);

const pipe = (f, ...fs) => (...as) => go(f(...as), ...fs)
console.log(f(0,1)); # 111
```



<b>curry</b>

> 코드를 값으로 다루면서 받아둔 함수를 원하는 때에 평가되도록 하는 함수.

```javascript
const curry = f => (a, ..._) => _.length ? f(a, ..._) : (..._) => f(a, ..._);
# 받아온 인자가 2개 이상이면 받아온 함수를 즉시 실행하고, 인자가 2개 보다 작으면 함수를 다시 리턴하고 그 이후에 받은 인자로 함수를 실행하는 함수. 표현이 어렵지만 코드를 읽으면 괜찮다.


# ex_1
const mult = curry((a,b) => a*b);
console.log(mult(1)(2)) # 2 (1*2)

const mult3 = mult(3)

console.log(mult3(3)) # 9 (3*3)
console.log(mult3(5)) # 15 (3*5)
console.log(mult3(10)) # 30 (3*10)

# 이러한 curry함수를 통해 앞서 만든 함수를 간단하게 할 수 있다.
go(
    products,
    products => filter(p=> p.price < 300, products),
    products => map(p=> p.price, products),
    prices => reduce(add, prices),
    console.log
)

go(
    products,
    curry(filter(p=> p.price < 300),
    curry(map(p=> p.price),
    curry(reduce(add),
    console.log
)

```



- <b>함수의 조합으로 함수 만들기</b> 

```javascript
go(
    products,
    curry(filter(p=> p.price < 300),
    curry(map(p=> p.price),
    curry(reduce(add),
    console.log
);
# 위 두 함수에 중복되는 코드를 함수의 조합을 통해 간단하게 만드려고 한다.
go(
    products,
    curry(filter(p=> p.price >= 300),
    curry(map(p=> p.price),
    curry(reduce(add),
    console.log
);

# 중복되는 함수를 하나의 함수로 조합한다.
const total_price = pipe(
	map(p=>p.price),
	reduce(add)
)


go (
	products,
	filter(p=>p.price<300)
	total_price,
	console.log
)

go (
	products,
	filter(p=>p.price>=300)
	total_price,
	console.log
)

# 또한 인자만 따로 받아서 하나의 함수로 만들 수 있다.
const base_total_price = predi => pipe(
	filter(predi),
	total_price
)

go(
	products,
	base_total_price(p=>p,price < 300),
	console.log
)
go(
	products,
	base_total_price(p=>p,price >= 300),
	console.log
)

```



