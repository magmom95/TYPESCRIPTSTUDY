![header](https://capsule-render.vercel.app/api?type=waving&color=auto&height=300&section=header&text=타입스크립트%20정리%20&fontSize=90&animation=fadeIn&fontAlignY=38&desc=%20이성규&descAlignY=65&descAlign=90)

# 타입스크립트 이것저것 정리

📌 굳이? 타입스크립트 쓰는 이유?

- 자바스크립트는 Dynamic typing 을 지원하는 언어이므로 대규모 프로젝트 경우에 오류를 찾기 힘듬

✔ Dynamic typing 이란

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
