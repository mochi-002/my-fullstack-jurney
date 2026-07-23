# [Intro & Type Annotations](https://elzero.org/typescript-assignments-lessons-from-1-to-11/)

## Assignment no.1
```json
// File Layout
"rootDir": "./project/files/typescript",
"outDir": "./dist/compiled/javascript"
  
// Other Outputs
"sourceMap": true,
```

## Assignment no.2
```ts
function calculate(numOne: number, numTwo: number) {
    return numOne + numTwo;
}

console.log(calculate(10, 20)); // 30
// console.log(calculate("10", "20")); // We Don't Need This To Work
console.log(calculate(+true, +true)); // 2
```

## Assignment no.3
```ts
function printInfo(valueOne: number | string, valueTwo: number | string): string {
    return `Value One Is ${valueOne}, Value Two Is ${valueTwo}`;
}

console.log(printInfo(10, 20)); // Value One Is 10, Value Two Is 20
console.log(printInfo("10", "20")); // Value One Is "10", Value Two Is "20"
console.log(printInfo(true, [1, 2, 3])); // We Don't Need This To Work

```

## Assignment no.4
```ts
let arr: (number | boolean[] | (string | (string | number)[])[])[] = [1, [true, false], ['string', ["string", 1]]];
```

## Assignment no.5
```json
"noImplicitAny": false,
"noUnusedLocals": true,
"noUnusedParameters": true,
"allowUnreachableCode": false,
```

## Assignment no.6
```ts
console.log(showMyDetails(theName, theName, nothing)); // Elzero
```

## Assignment no.7
```ts
function showMsg(user?: number | string, age?: boolean | number | string, country?: boolean | string) {
    return `${user}${age}${country}`;
}
```

## Assignment no.8
```ts
function printInConsole(...arg: (number | string | boolean)[]) : string{
    arg.forEach(e => { 
        console.log(`The Value is ${e} And Type Is ${typeof e}`);
    });
    return `Done`
}
```

---
# [Data Types](https://elzero.org/typescript-assignments-lessons-from-12-to-21/)

## Assignment no.1
```ts
type n = number;
```

## Assignment no.2
```ts
type mix = number | boolean
```

## Assignment no.3
```ts
type Info = {
    theName: string,
    theAge: number
}

type Full = Info & {
    country: string
}
```

## Assignment no.4
```ts
function yesOrNo(val: number): "True" | "False" {
    return (val > 10) ? "True" : "False";
}
```

## Assignment no.5
```ts
type custom = "Yes" | "No";
function isHeOld(age: number | string): custom | number {
    if (typeof age === "string") {
        throw new Error("Error");
    }
    return age > 40 ? "Yes" : "No";
}
```

## Assignment no.6
```ts
let post: readonly [number, string, boolean];
const [id, title, state] = post
```

## Assignment no.7
```ts
function getInsane (num:number) :number {
    return Game.Hard - num;
}

enum Game {
    Easy = 100,
    Medium = Game.Easy - 20,
    Hard = Game.Medium - (Game.Easy / 2),
    Insane = getInsane(10)
}
```

## Assignment no.8
```ts
const user: {
    username: string,
    age: number | string,
    website?: string,
    skills: {
        frontEnd: string[],
        backEnd: (string | number)[]
    }
```
---
# [Interfaces & Class Part 1](https://elzero.org/typescript-assignments-lessons-from-22-to-31/)

## Assignment no.1
```ts
interface Member {
    id: number | string;
    username: string;
    country?: string;
    state: boolean;
    getName: () => string
}
```

## Assignment no.2
```ts
interface Client {
    id: number,
    username: string,
    active: boolean,
    discount: number,
    getPrice: (n: number) => number
}
```

## Assignment no.3
```ts
interface Superman extends Man, Bird {
    bodyType: string,
    origin: string
}
```

## Assignment no.4
```ts
class Player {
    constructor(
        public username: string,
        public type: string,
        power: number | string,
        public available?: boolean
    ) {
        this.power = Number(power);
    }

    public power: number;

    details(): string {
        return `${this.available ? "VIP " : ""}${this.username}, Type Is ${this.type} Level Is ${this.power}`;
    }
}
```

## Assignment no.5
```ts
class Shorten {
    constructor(public id: number, public username: string, protected title: string) {
    }
}
```

## Assignment no.6
```ts
class Show {
    public get title(): string {
        return this._title;
    }
    public set title(value: string) {
        this._title = value;
    }
    constructor(private _title: string) { }
}
```

## Assignment no.7
```ts
class Player implements Play {
    constructor(
        public id: number,
        public title: string,
        public level: number | string,
    ) { }
    logIn(): void {
        console.log(`Logged In`)
    }
    logOut(msg: string): void {
        console.log(`Logged Out, ${msg}`)
    }
}
```
---
# [Class Part 2 And Generics](https://elzero.org/typescript-assignments-lessons-from-32-to-38/)

## Assignment no.1
```ts
class RPG extends Game {
    constructor(title: string, price: numandstring, public rate: number) {
        super(title, price);
    }
    override getLocation(): string {
        return "Location"
    }
    override getDiscount(): string {
        return "Discount"
    }
}

class Action extends Game {
    constructor(title: string, price: numandstring, public rate: number, public company: string) {
        super(title, price);
    }
    override getLocation(): string {
        return "Location"
    }
    override getDiscount(): string {
        return "Discount"
    }
}
```

## Assignment no.2
```ts
function showTypes<T = string, U = number, V = boolean>(
  value1?: T,
  value2?: U,
  value3?: V
): string {
  return `${value1 ?? "Nothing"} - ${value2 ?? "Nothing"} - ${value3 ?? "Nothing"}`;
}
```

## Assignment no.3
```ts
class Game<T> {
    constructor(
        public title:T,
        public price:number
    ) { }

    getDiscount(dis: T):void {
            console.log(`The Discount Is ${dis}`);
    }
}
```
---