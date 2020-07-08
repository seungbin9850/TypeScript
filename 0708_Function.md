# 0708_Function

TypeScript는 JavaScript와 마찬가지로 기명 함수와 익명 함수를 지원함.

## 함수 타이핑

``` typescript
function add(x: number, y: number): number {
    return x + y;
}

let myAdd = function(x: number, y: number): number { return x + y };
```
각 파라미터와 함수의 반환 타입을 정해줄 수 있다.

---

## 함수 타입 작성

함수 자체의 타입을 함수 타입이라고 한다.

``` typescript
let myAdd: (x: number, y: number) => number = (x, y) => { return x + y }; 
```

위 그림은 익명 함수의 타입으로 함수 타입을 선언함

익명 함수의 타입을 함수 타입으로 분리하면 새로 정의한 타입은 반복적으로 재활용 가능

``` typescript
type calcType = (a: number, b: number) => number;
```
함수 타입을 type 앨리어스를 이용해 별도로 분리해 사용할 수 있다.

calcType은 익명 함수를 할당받는 여러 변수에함수 타입으로 선언할 수 있다.

``` typescript
type calcType = (a: number, b: number) => number;
let addCalc: calcType = (a, b) => a + b;
```
---

## 선택적 매개변수

TypeScript에선 선택적 매개변수를 원할 때 매개변수 이름 끝에 ? 를 붙여 사용할 수 있다.

``` typescript
function buildName(firstName: string, lastName?: string) {
    if (lastName) return firstName + " " + lastName;
    else return firstName;
}
```
매개변수의 값을 지정해 줄 수도 있다.

``` typescript
function buildName(firstName: string, lastname: "last") {
    return firstName + " " + lastName
}
```

## 나머지 매개변수

다수의 매개변수를 그룹지어 사용하고 싶을 때 사용

나머지 매개변수는 "..." 형태로 선언함

``` typescript
function colors(a: string, ...rest: string[]) {
    return a + " " + rest.join(" ");
}

let color1 = colors("red"); // red
let color2 = colors("red", "orange"); // red orange
let color3 = colors("red", "orange", "yellow"); // red orange yellow
```

## 함수 오버로드

함수명은 같지만 매개변수와 반환 타입이 다른 함수

``` typescript
function add(a: string, b: string): string;
function add(a: number, b: number): number;
function add(a: any, b: any): any {
    return a + b;
}
```

가장 일반적인 함수 (매개변수 any)의 시그니처를 가장 아래 선언하고, 그 위로 구체적인 타입을 명시해야 함.

이 때, 매개변수가 다른 오버로드를 지정할 때는 선택 매개변수를 둬 매개변수 수에 변화를 줌

``` typescript
function add(a: number): number;
function add(a: number, b: number): number;
function add(a: any, b?: any): any {
    if (b === undefined) return a;
    else return a + b;
}
```