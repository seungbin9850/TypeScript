# 0709_Interface

인터페이스는 타입이며 컴파일 후에 사라진다.

선언만 존재함.

멤버 변수와 멤버 메서드를 선언할 수 있지만 접근 제한자는 설정할 수 없다.

``` typescript
interface Car {
    speed: number;
}
```

자식 인터페이스는 extends 키워드를 이용해 부모 인터페이스를 상속받을 수 있다.

인터페이스는 다중 상속이 가능하다.

``` typescript
interface Car {
    speed: number;
}

interface SportsCar {
    acceleration: number;
}

interface MyOptimizedCar extends Car, SportsCar {
    waterproof: boolean;
}

let MyCar = <MyObtimizedCar>{};
myCar.speed = 100;
myCar.acceleration = 100;
myCar.waterproof = true;
```

만약 다중 상속을 받을 때 같은 이름의 메서드를 상속받으면, 같은 이름의 메소드를 모두 재정의 해줘야 한다.

``` typescript
interface Dog {
    run(): void;
    getStatus(): { runningSpeed: number; };
}

interface Bird {
    fly(): void;
    getStatus(): { flightSpeed: number; };
}

interface DogBird extends Dog, Bird {
    getStatus(): { runningSpeed: number, flightSpeed: number; }
}
```
같은 getStatus() 메소드지만, 반환 타입이 달라 재지정 해 주었다.

인터페이스 정의를 마치면 implements 키워드를 이용해 인터페이스를 구현해야한다.

``` typescript
class NewAnimal implements DogBird {
    run(): void { }
    fly(): void { }
    getStatus(): { runningSpeed: number, flightSpeed: number; } {
        return { runningSpeed: 10, flightSpeed: 20 }
    }
}
```
---
인터페이스의 프로퍼티를 읽기 전용으로 선언할 수 있다.
``` typescript
interface Point {
    readonly x: number;
    readonly y: number;
}

let p1: Point { x: 10, y: 20 };
p1.x = 5; // 오류 발생
```
---
인터페이스로 함수 타입을 기술할 수 있다.

``` typescript
interface SearchFunc {
    (source: string, subString: string): boolean;
}
let mySearch: SearchFunc = function(src, sub) {
    let result = src.search(sub);
    return result > -1;
}
```