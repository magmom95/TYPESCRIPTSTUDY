![header](https://capsule-render.vercel.app/api?type=waving&color=auto&height=300&section=header&text=타입스크립트%20정리%20&fontSize=90&animation=fadeIn&fontAlignY=38&desc=%20이성규&descAlignY=65&descAlign=90)

# 타입스크립트 이것저것 정리

📌 굳이? 타입스크립트 쓰는 이유?

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
