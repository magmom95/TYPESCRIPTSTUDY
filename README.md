![header](https://capsule-render.vercel.app/api?type=waving&color=auto&height=300&section=header&text=타입스크립트%20정리%20&fontSize=90&animation=fadeIn&fontAlignY=38&desc=%20이성규&descAlignY=65&descAlign=90)

# 타입스크립트 이것저것 정리

📌 굳이 타입스크립트 쓰는 이유?

- 자바스크립트는 Dynamic typing 을 지원하는 언어이므로 대규모 프로젝트 경우에 오류를 찾기 힘듬

✔ Dynamic typing 이란?

- 런타임에 타입이 결정되는 언어 즉, 소스가 빌드될 때 자료형을 결정하는 것이 아니라 실행 시 결정

- 매번 타입을 써줄 필요가 없기 때문에 프로그래머가 빠르게 코드를 작성할 수 있음

- 런타임까지 타입에 대한 결정을 끌고 갈 수 있기 때문에 선택의 여지가 있음

- 실행 도중에 변수에 예상치 못한 타입이 들어와 Type Error가 발생하는 경우가 생길 수 있음

🚩 대규모 프로젝트에서 오류가 났을때 타입스크립트는 Dypnamic 하지 않으므로 오류를 친절하게 알려줌

---
<details markdown="1">
<summary>✨ 타입 정하기</summary>
<br>

- **타입스크립트**는 **변수**만들 때 **변수의 타입** 지정 가능

``` javascript
    let test : string = 'lee'
```

- 🎉변수명:타입 으로 설정!

- test 라는 변수는 string 타입이 됨

``` javascript
    let test1 : string[] = ['lee', 'kim']
```

- array 자료들은 **타입명[]** 으로 지정 

``` javascript
    let test2 : {age : number} = { age : 20 }
```

- object 자료들은 **{}** 으로 똑같은 모습으로 타입을 지정

⚠ 위 처럼 타입스크립트를 지정을 하게 되면 귀찮으므로 하지 않음 (자동 부여 됨)

``` javascript
    let name = 'Lee';
    let age = 28;
```

- 이렇게 하면 자동으로 타입이 지정 됨

``` javascript
    let name ;
    let name = 'Lee';
```

- 이렇게 해도 가능


</details>

---

<details markdown="1">
<summary>❓ 타입을 미리 정하기 애매할 때</summary>

- 타입 정하기 어려우면 **union type** 을 사용

``` javascript
    let name: string | number = 'Lee';
    let age: (string | number) = 28;
```

- 할당하는 순간 object 자료에 number string이 들어옴

``` javascript
    var array: (number | string)[] = [1,'2',3]
    var object: {data : (number | string) } = { data : '123' }
```

- array, object에 정의된 Union 타입은 OR 연산자가 유지

⚠ any 타입도 존재 

``` javascript
    let name: any = 'Lee';
    name = 123;
    name = undefined;
    name = [];
```

- 에러가 나지 않지만 실드를 안씌우는 효과를 줌

- 변수 타입체크 해제기능 용도로만 사용 

✔ any 보다는 unknown 타입

``` javascript
    let name: unknown = 'Lee';
    name = 123;
    name = undefined;
    name = [];
```

- 1. unknown 타입엔 모든 자료 다 집어넣을 수 있음

- 2. 자료집어넣어도 타입은 그대로 unknown

📌 이 코드는 오류

``` javascript
    let age: unknown = 1;
    age + 1;
```

- unkown은 새로운 타입을 하나 만드는것 (즉 number 타입이 아니라 연산 불가)

- union type도 이 동일

</details>

---

<details markdown="1">
<summary> 📐함수 형식</summary>

<br>

- 함수는 총 두 군데 타입지정 가능 

1. 함수로 들어오는 자료 (파라미터)

2. 함수에서 나가는 자료 (return)

``` javascript
    function test(x :number) :number { 
    return x * 2 
} 
```

1. 함수로 들어오는 파라미터 타입지정은 파라미터 옆에 적으면 됨

2. 함수가 실행된 후 남는 값 (return 우측에 있는 값) 타입지정하고 싶으면 함수명() 우측에 적으면 됨

``` javascript
    function test(x :number) :void { 
  return x * 2 //여기서 에러남 
} 
```

- return 값이 없을 때

``` javascript
    function test(x? :number) { 

} 
```

- 옵션도 가능 (x : number | undefined 라는 의미)

``` javascript
    function test(x :number | string) :number { 
    return x.toString().length 
} 
```

- 자릿수 세기 함수

</details>

---

<details markdown="1">
<summary>🏴 Type Narrowing</summary>

<br>

- if문 등으로 타입을 하나로 정해주는 것

``` javascript
    function test(x :number | string){
      if (typeof x === 'number') {
        return x + 1
      } 
      else if (typeof x === 'string') {
        return x + 1
      }
      else {
        return 0
          }
        }
    } 
```

- if문과 typeof 키워드로 현재 파라미터의 타입을 검사 

- 꼭 typeof를 쓸 필요는 없고 타입을 하나로 확정지을 수 있는 코드라면 어떤 것도 Narrowing 역할 가능 (in, instanceof 사용가능)

``` javascript
    function test(x :number | string){ 
        return (x as number) + 1 
    }
    console.log( test(123) )
```

- as를 통해 타입 변경 가능

1. as 키워드는 union type 같은 복잡한 타입을 하나의 정확한 타입으로 줄이는 역할을 수행 (number 타입을 as string 이렇게 바꾸려고 하면 에러남)

2. 실은 그냥 타입실드 임시 해제용 실제 코드 실행결과는 as 있을 때나 없을 때나 거의 동일

✔ as는 타입을 실제로 바꿔 주는 역할이 아님

⚠ as는 언제 사용 하는가?

1. 왜 타입에러가 나는지 정말 모르겠는 상황에 임시로 에러 해결용으로 사용하거나

2. 내가 어떤 타입이 들어올지 정말 확실하게 알고 있는데 컴파일러 에러가 방해할 때 사용

</details>

---

<details markdown="1">
<summary>💢 타입 정의가 너무 길면?</summary>

<br>

``` javascript
let test :string | number | undefined;
```

- 이게 길고 보기 싫거나 재사용을 하고 싶을 때 = **변수**에 담아 사용 (**type alias**)

``` javascript
type test :string | number | undefined;
let go :test;
```

- **type 타입변수명 = 타입종류** 로 표현

- object 타입도 저장 가능

``` javascript
type friend = {
  readonly name : string,
}

let test :friend = {
  name : 'Lee'
}

test.name = 'lee' //readonly라서 에러남
```

- readonly 키워드는 속성 왼쪽에 붙여 속성을 변경불가능하게 잠금

``` javascript
type Name = string;
type Age = number;
type NewOne = Name | Age;
```

- 물음표 연산자(undefined 라는 타입), Union type도 가능

``` javascript
type Name = string;
type Name = number;
```

- type 재정의는 불가 

</details>

---

<details markdown="1">
<summary>🚩 Const 변수 유사품</summary>

<br>

``` javascript
var book = {
  name : 'lee'
}

function test(a : 'lee') {

}
test(book.name)
```

- 오류가 남 ( **lee** 타입만 입력할 수 있다고 해놨고 **book.name** 이라는건 string 타입이지 **lee**타입이 아니기 떄문!!)

- 해결 방법

1. object 만들 때 타입을 잘 미리 정하든가 

2. assertion을 사용

3. 아니면 as const 라는걸 애초에 object 자료에 붙임

``` javascript
var book = {
  name : 'lee'
} as const;

function test(a : 'lee') {

}
test(book.name)
```

- as const 효과가 2개 

1. 타입을 object의 value로 바꿔 줌 (타입을 'lee'으로 바꿔 줌)

2. object안에 있는 모든 속성을 readonly로 바꿔 줌 (변경하면 에러나게)

✔ object를 잠그고 싶으면 as const

- Function type 도 저장 가능

``` javascript
type NumOut = (x : number, y : number ) => number ;
```

- 이런 식으로 함수도 저장 가능

``` javascript
type NumOut = (x : number, y : number ) => number 
let ABC :NumOut = function(x,y){
  return x + y
}
```

- 응용 가능

</details>

---

<details markdown="1">
<summary>🎨 함수와 methods에 type alias 지정</summary>

<br>

``` javascript
type NumOut = (x : number, y : number ) => number ;
}
```

- 이런 식으로 표현 가능

``` javascript
type NumOut = (x : number, y : number ) => number ;
let ABC :NumOut = function(x,y){
  return x + y
}
```

- **함수명 : 타입별명** 으로 선언

``` javascript
let member = {
  name : 'lee',
  age : 28,
  plusOne (x){
    return x + 1
  },
  changeName : () => {
    console.log('안녕')
  }
}
member.plusOne(1);
member.changeName();
}
```

- 함수도 자료안에 보관하고 싶을 때 사용

``` javascript
class Person {
  data :number = 0;
}

let lee = new Person();
lee.data = '1';  //문자 할당시 에러
```

- class 형식도 가능

``` javascript
class Person {
  name;
  age;
  constructor ( a :string ){
    this.name = a;
    this.age = 28;
  }
}
```

- constructor 타입 지정

``` javascript
class Person {
  
  add(숫자){
    console.log(숫자 + 1)
  }
}
```

- methods 타입지정

</details>

---

<details markdown="1">
<summary>🐱‍🐉 Object에 쓸 수 있는 interface </summary>

<br>

``` javascript
interface Square { 
  color :string, 
  width :number, 
} 

let test :Square = { color : 'red', width : 100 } 

```

- type을 정의할 때 interface를 사용 가능

- 대문자로 작명하고 {} 안에 타입을 명시 

✔ interface 장점은 extends가 가능 (상속)

``` javascript
interface Student {
  name :string,
}
interface Teacher extends Student {
  age :number
}
} 
```

⚠ type 선언과 interface에 차이점

- **type**은 새로운 속성을 추가하기 위해서 다시 같은 이름으로 선언할 수 없지만, **interface**는 항상 선언적 확장이 가능

``` javascript
interface Window {
  title: string
}

interface Window {
  ts: TypeScriptAPI
}

// 같은 interface 명으로 Window를 다시 만든다면, 자동으로 확장이 됨

const src = 'const a = "Hello World"'
window.ts.transpileModule(src, {})
```

``` javascript
type Window = {
  title: string
}

type Window = {
  ts: TypeScriptAPI
}

// Error: Duplicate identifier 'Window'.
// 타입은 안됨
```

</details>

---

<details markdown="1">
<summary>🐱‍👤 never타입 이란?</summary>

<br>

``` javascript
function 함수() :never{
  while ( true ) {
    console.log(123)
  }
}
```

- 조건 1) 절대 return을 하지 않아야하고 (void같은거)

- 조건 2) 함수 실행이 끝나지 않아야합니다 (전문용어로 endpoint가 없어야 함)

</details>

---

<details markdown="1">
<summary>📸 Generic타입 이란?</summary>

<br>

``` javascript
function test(x: unknown[]) {
  return x[0];
}

let a = test([4,2])
console.log(a) 
```

- array도 unknown 타입이라 4가 출력

``` javascript
function test(x: unknown[]) {
  return x[0];
}

let a = test([4,2])
console.log(a + 1) 
```

- unknown 타입이라 연산도 에러 그래서 나온것이 Generic 함수

``` javascript
function test<T>(x: T[]) :T {
  return x[0];
}

let a = test<number>([4,2])
let b = test<string>(['kim', 'park']) 
```

- Generic을 쓰면 여러분이 정한 타입을 return 값으로 뱉는 함수를 제작가능

``` javascript
function test<T>(x: T) {
  return x - 1
}

let a = test<number>(100)
```

- return 문에 혹시 다른문자가 나오면 에러가 나옴

``` javascript
function test<T extends number>(x: T) {
  return x - 1
}

let a = test<number>(100)
```

- T extends number 를 사용 타입 파라미터에 넣을 수 있는 타입을 제한 

``` javascript
interface lengthCheck {
  length : number
}
function test<T extends lengthCheck>(x: T) {
  return x.length
}

let a = test<string>('hello')  //가능
let a = test<number>(1234) //에러남
```

- extends 를 통해 length 속성을 복사해서 가짐

- length가 분명히 있기 때문에 x는 .length 조작이 가능 함

</details>

---

<details markdown="1">
<summary>🎆 React에 typescript를 적용</summary>

<br>

```shell
npx create-react-app 프로젝트명 --template typescript 
```

- 리액트 프로젝트를 설치하면서 타입스크립트를 사용

```shell
npm install --save typescript @types/node @types/react @types/react-dom @types/jest
```

- 이미 만든 프로젝트는 보는거와 같이 작성

![image](https://user-images.githubusercontent.com/64140544/159925935-c9d34ab8-5b49-464b-87a8-d5169c993da2.png)

- 위와 같이 파일들이 형성 

1. 일반 변수, 함수 타입 지정은 기존과 같음

2. JSX 타입지정

``` javascript
let box :JSX.Element = <div></div>
let button :JSX.Element = <button></button>
```
    
``` javascript
let box :JSX.IntrinsicElements['div'] = React.createElement('div');
let button :JSX.IntrinsicElements['button'] = <button></button>;
```

3. function component 타입 지정

``` javascript
type AppProps = {
  name: string;
}; 

function App (props: AppProps) :JSX.Element {
  return (
    <div>{message}</div>
  )
}
// <div> <a> <h4> 같은 기본 태그들은 JSX.IntrinsicElements 라는 이름의 타입을 사용
```

4. state 문법 사용시 타입지정 

``` javascript
const [user, setUser] = useState<string | null>('lee'); 
// <>Generic문법을 이용 useState함수에 집어넣음
```

5. type assertion 문법 사용할 때 

``` javascript
let code: any = 123; 
let employeeCode = <number> code; //안됨
```

🎇 redux에 typescript를 적용하는 법

``` javascript
import { Provider } from 'react-redux';
import { createStore } from 'redux';

interface Counter {
  count : number
}

const 초기값 :Counter  = { count: 0 };

function reducer(state = 초기값, action :any) {
  if (action.type === '증가') {
    return { count : state.count + 1 }
  } else if (action.type === '감소'){
    return { count : state.count - 1 }
  } else {
    return initialState
  }
}

const store = createStore(reducer);

// store의 타입 미리 export 해두기 
export type RootState = ReturnType<typeof store.getState>

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
) 
```

- state를 꺼낼 때

``` javascript
import React from 'react';
import { useDispatch, useSelector } from 'react-redux'
import { Dispatch } from 'redux'
import {RootState} from './index'

function App() {
  const 꺼내온거 = useSelector( (state :RootState) => state );
  const dispatch :Dispatch = useDispatch();

  return (
    <div className="App">
      { 꺼내온거.count }
      <button onClick={()=>{dispatch({type : '증가'})}}>버튼</button>
      <Profile name="kim"></Profile>
    </div>
  );
} 
```

- 신규방식 redux

```shell
npm install @reduxjs/toolkit  
```

- 이런식으로 표현 가능

``` javascript
import { createSlice, configureStore } from '@reduxjs/toolkit';
import { Provider } from 'react-redux';

const 초기값 = { count: 0, user : 'kim' };

const counterSlice = createSlice({
  name: 'counter',
  initialState : 초기값,
  reducers: {
    increment (state){
      state.count += 1
    },
    decrement (state){
      state.count -= 1
    },
    incrementByAmount (state, action :any){
      state.count += action.payload
    }
  }
})

let store = configureStore({
  reducer: {
    counter1 : counterSlice.reducer
  }
})

//state 타입을 export 해두는건데 나중에 쓸 데가 있음
export type RootState = ReturnType<typeof store.getState>

//수정방법 만든거 export
export let {increment, decrement, incrementByAmount} = counterSlice.actions
```

- 타입 지정은 아래와 같음

1. state 초기값 타입지정 알아서 

2. reducer 안의 action 파라미터의 타입지정

3. 나머지는 자동 

- action 타입은 아래와 같이 지정  

```javascript
import { createSlice, PayloadAction } from '@reduxjs/toolkit'

(상단 생략)
  incrementByAmount (state, action: PayloadAction<number>){
      state.value += action.payload
  },
```

- state를 꺼낼 때 

```javascript
import { useDispatch, useSelector } from 'react-redux'
import {RootState, increment} from './index'

function App() {

  const 꺼내온거 = useSelector( (state :RootState) => state);
  const dispatch = useDispatch();

  return (
    <div className="App">
      {꺼내온거.counter1.count}
      <button onClick={()=>{dispatch(increment())}}>버튼</button>
    </div>
  );
} 

```

1. useSelector 함수를 쓰면 state를 쉽게 꺼낼 수 있음

- state가 어떻게 생겼는지 파악한 다음 타입알아서 손수 지정

- index.ts에서 타입을 export 해서 가져 옴 

- index.ts 에 있던 export type RootState = ReturnType<typeof store.getState> 가 store의 타입을 미리 export 해두는 방법
    
2. useDispatch 함수를 쓰면 쉽게 수정요청을 날릴 수 있음

- import {Dispatch} from 'redux' 이렇게 타입을 가져와서 const dispatch :Dispatch 

- dispatch 날릴 때 안에 파라미터 안쓰면 에

</details>

---
