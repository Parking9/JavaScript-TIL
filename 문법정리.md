# 1013 Workshop
## JavaScript 문법 정리


### 1. 변수

- let : 값을 재할당 할 수 있는 변수 선언 키워드
- const : 값이 변하지 않는 상수 변수 선언 키워드

**공통점 : 블록 유효범위를 가짐, 재선언 불가**

### 2. 타입과 연산자
#### 2-1. 타입
- Number : 일반적인 숫자 타입, -Infinity, NaN도 Number타입
- Boolean : true, false
- Empty Value : null (값이 없음을 표현하기 위해 할당), undefined(값이 없음) *typeof ---*을 통해 서로 다름을 확인

#### 2-2. 연산자
- 할당 연산자 : =, -, *, ++, --
- 비교 연산자 : 문자열 비교에서 소문자가 대문자 보다 크다.
- **동등 연산자 (==)** : 비교 대상이 서로 다른 타입일 경우, 비교하기 전에 같은 자료형으로 자동 변환하여 비교한다.
- 비교 연산자 (===) : 타입과 값이 같은지 모두 비교
- 논리 연산자 : && (and), || (or), ! (not)
- 삼항 연산자 : 조건의 true, false에 따라 다른 값을 반환하는 연산
ex) Math.PI > 4 `?` true일때 반환값 : false일때 반환값


### 3. 조건문과 반복문
#### 3.1 조건문
- `if () {}`, `else if () {}`, `else {}`
- `switch` 하나의 표현식을 평가하여 일치하는 case 절을 실행 없으면 default절 실행, 각 case에 break를 넣어주지 않으면 default절까지 실행됨.
```javascript
switch(name){
    case 'jun': {
        console.log('Hi, Jun')
        break
    }
    case 'Kim':{
        console.log('Hi,Kim')
        break
    }
    case default:{
        console.log(`${name}님 환영합니다.`)
        // 파이썬의 f스트링 -> `(백틱)${변수명}`
    }
}
```
#### 3.2 반복문
- while : `while (조건) {}`
- for : `for (let i=0; i <6; i++>){}`
- for of : 배열에서 요소를 순회하면 반복하는 반복문. 매 요소는 블럭 내에서 새롭게 선언되므로 반드시 변수 선언 키워드가 필요
```javascript
const numbers=[1,2,3,4]

for (const number of number){
    console.log(number)
}
```
- for in : Object의 key를 순회하며 반복하는 반복문. *Array의 경우 index를 순환한다.*
```javascript
const fruits = {a: 'apple', b: 'banana'}
for ( const key in fruits){
    console.log(key)
    console.log(fruits[key])
}
```

### 4. 함수
- 함수 선언식
```javascript
이름이 없는 함수로 익명함수.
function add (num1, num2){
    return num1+num2
}
add(2,7) //9
```

- 함수 표현식
JS에서는 함수를 일급 객체로 취급하기 때문에 함수를 매개변수로 넘기거나 변수에 담아서 사용할 수 있다.
```javascript
const sub = function (num1, num2){
    return num1+num2
}
sub(2,3) //5
```

- 기본인자 (default 전달)
```javascript
const hello = function (name='홍싸피'){
    console.log(`${name}님 헬로`)
}
hello() //홍싸피님 헬로
```

- **화살표 함수** : fuction키워드와 중괄호를 생략하며 함수 선언
```javascript
// 항상 익명이기 때문에 '함수 표현식'에서만 선언할 수 있다.
const arrow = function (name) {
  return `hello! ${name}`
}

// 1. function 키워드 삭제
const arrow = (name) => { return `hello! ${name}` }

// 2. () 생략 : 매개변수 하나인 경우
const arrow = name => { return `hello! ${name}` }

// 3. {} & return 생략 : 바디 표현식이 하나인 경우
const arrow = name => `hello! ${name}`

// 4. 매개변수 없는 경우
const arrow = () => console.log('안녕!')
```

### 5. 자료구조 (Array와 Object)
#### 5.1 Array(배열)
```javascript
const numbers = [1, 2, 3, 4]

numbers[0]     // 1
numbers[-1]    // undefined => 정확한 양의 정수 index만 가능
numbers.length // 4
```

#### 자주 쓰이는 배열의 메서드

* `reverse`

  * 원본 배열의 요소 순서를 반대로 정렬한다.

  ```javascript
  numbers.reverse()
  numbers  // [4, 3, 2, 1]
  
  numbers.reverse()
  numbers  // [1, 2, 3, 4]
  ```

* `push & pop`

  * 요소를 배열 가장 뒤에 추가하거나 제거한다.

  ```javascript
  numbers.push('a')  // 5 => 새로운 배열의 길이
  numbers  // [1, 2, 3, 4, 'a']
  
  numbers.pop()  // 'a' => 가장 마지막 요소
  numbers  // [1, 2, 3, 4]
  ```

* `unshift & shift`

  * 요소를 배열 가장 앞에 추가하거나 제거한다.

  ```javascript
  numbers.unshift('a')  // 5, 새로운 배열의 길이
  numbers  // ['a',1,2,3,4]
   
  numbers.shift()  // 'a', 가장 처음 요소
  numbers  // [1,2,3,4]
  ```

* `includes`

  * 배열에 특정 요소가 있는지 여부를 boolean 값으로 반환한다.

  ```javascript
  numbers.includes(1)  // true
  numbers.includes(0)  // false
  ```

* `indexOf`

  * 배열에 특정 요소가 있는지 여부를 확인한 후, 가장 처음 찾은 요소의 index 값을 반환한다.
  * 요소가 없으면 `-1`을 반환한다.

  ```javascript
  numbers.push('a', 'a')
  numbers  // [1,2,3,4,'a','a']
  numbers.indexOf('a')  // 4
  numbers.indexOf('b')  // -1
  ```

* `join`

  * 배열의 요소를 함수의 인자를 기준으로 이어서 문자열로 반환한다.
  * 인자가 없으면 `,` 문자를 기준으로 이어서 문자열을 반환한다.
  * 원본은 바뀌지 않는다.

  ```javascript
  numbers.join()    // '1,2,3,4,a,a'
  numbers.join('')  // '1234aa'
  numbers.join('-') // '1-2-3-4-a-a'
  ```

#### 5.2 Obejct(객체)

Object의 key는 문자열 타입, value는 모든 타입이 될 수 있다.

```javascript
const me = {
  name: '김효진',
  'phone number': '010-0000-0000',
  sayHello: function () {
    console.log('난 효진이야!')
  },
  appleProducts: {
    ipad: '2020Pro',
    iphone: 'XS',
    macbook: '2019Pro',
  },
}
```

- Object 축약 문법
객체를 정의할 떄 key와 할당하는 변수의 이름이 같으면 축약가능
```javascript
const name = 'Ronaldo'
const score = '-100'

const student={
    name,
    score,
    // name : name,
    // score : score,
}
```
- Object Destructuring
객체 및 배열 리터럴 표현식을 사용하면 즉석에서 쉽게 데이터 뭉치를 만들 수 있습니다.
```javascript
var foo = ["one", "two", "three"];

var [one, two, three] = foo;
console.log(one); // "one"
console.log(two); // "two"
console.log(three); // "three"
```

#### 5.3 JSON (JavaScript Object Notation, JS객체 표기법)
> key-value 형태로 JS Object와 유사한 모습으로 데이터를 표현하는 표기법
>
> 모습만 비슷할 뿐이고, 실제로는 문자열 타입이다.
>
> Object처럼 사용하기 위해선 Parsing(구문 분석) 작업이 필요하다.
>
> JSON 형식의 파일을 다루기 위해 JS에서는 JSON 내장 객체를 제공한다.


##### Object -> JSON(string)

```javascript
const jsonData = JSON.stringify({
  coffee: 'Americano',
  iceCream: 'Cookie and cream',
})

console.log(jsonData)
console.log(typeof jsonData)
```


##### JSON(string) -> Object

```javascript
const parsedData = JSON.parse(jsonData)

console.log(parsedData)
console.log(typeof parsedData)
```

#### 5.4 Array Help Method
> 자주 사용하는 로직을 재활용할 수 있게 만든 일종의 라이브러리

- **forEach**
주어진 callback 함수를 배열의 각 요소에 대해 한 번씩 실행한다.
  ```javascript
  const colors = ['red', 'blue', 'green']
  colors.forEach(function(color){
      console.log(color)
  })
  ```

- **map**
배열 내 모든 요소에 대해 주어진 callback 함수를 실행하며, 함수의 반환값을 요소로 하는 새로운 배열을 반환한다.

```javascript
const nums=[1,2,3]

const doubleNums=nums.map(function(num){
    return num *2
})
console.log(doubleNums) //[2,4,6]
```

- **filter**
주어진 callback 함수의 테스트를 만족하는 요소만으로 새로운 배열을 만든다.

```javascript
const product =[
    {name:'cucumber',type:'vege'},
    {name:'banana',type:'fruit'},
    {name:'carrot',type:'vege'},
    {name:'apple',type:'fruit'},
]
const fruits = product.filter(fuction(product){
    return product.type==='fruit'
})
console.log(fruits) //['banana','apple']
```

- **find**
주어진 callback 함수의 테스트를 만족하는 첫번째 요소를 반환한다. 없으면 undefined를 반환
```javascript
const avengers = [
{ name: 'Tony Stark', age: 45 },
{ name: 'Steve Rogers', age: 32 },
{ name: 'Thor', age: 40 },
]

const avenger = avengers.find(function (avenger) {
return avenger.name === 'Tony Stark'
})


// refactoring
const avenger = avengers.find(avenger => avenger.name === 'Tony Stark')

// console.log(avenger) {name: "Tony Stark", age: 45}
```

- **some**
배열 안의 요소 중 하나라고 callback 함수의 테스트를 만족하면 true를 반환하고 아니면 false를 반환한다. 빈 배열을 경우 false 반환

```javascript
const numbers = [1, 2, 3, 4, 5]

const result = numbers.some(function (number) {
return number === 3
})
```

- **every**
배열 안의 모든 요소가 callback 함수의 테스트를 만족하면 true를 반환, 아닐 경우 false를 반환한다. 빈 배열에서 호출 시 true를 반환한다.

```javascript
const numbers = [1, 2, 3, 4, 5]

const result = numbers.every(function (number) {
return number !== 0
})
```

- **reduce**
배열의 각 요소에 대해 주어진 callback 함수를 실행하고, 하나의 결과 값을 반환한다. reduce는 배열 내의 숫자 총합, 평균 계산 등 배열의 값을 하나로 줄이는 동작을 한다.

```javascript
arr.reduce(callback(acc, element, index, array), initialValue)
```

* map, filter 등 여러 배열 메서드의 동작을 대부분 대체할 수 있다.
* `acc` : 누적 값 (전 단계의 결과)
* `initialValue` : 반환할 누적 값의 초기 값 (없을 시 첫번째 요소 값이 누적 값이 된다)



* 예시

  ```javascript
  const numbers = [5, 5, 10, 7]
  
  const result = numbers.reduce(function (total, number) {
    return total + number
  })
  ```