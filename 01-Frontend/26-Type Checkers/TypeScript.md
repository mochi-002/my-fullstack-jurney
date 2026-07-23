# TypeScript Notes

## Why We Need TypeScript

1. Detect errors without running the code — "static type checking"
2. Analyze the code as you type
3. Saves some unit tests, since the error shows while writing
4. Every `.js` file is a valid `.ts` file
5. Helps when writing React, Vue, or Angular apps
6. Gives you features missing in JS, like interfaces, generics, and decorators

---

## Getting Started

### Install TypeScript

Globally via npm:

```bash
npm i -g typescript
```

Or on Arch Linux:

```bash
sudo pacman -S typescript
```

### Compile

Watch mode, recompiles on save:

```bash
tsc -w <filename>
```

### Project Config

Generate a `tsconfig.json`:

```bash
tsc --init
```

Recommended folder structure:

```text
-- dist
---- script
-------- index.js
-- src
---- index.ts
```

Key `tsconfig.json` options:

```json
{
  "rootDir": "./src",
  "outDir": "./dist/scripts"
}
```

---

## Static Types vs Dynamic Types

<table>
  <thead>
    <tr>
      <th></th>
      <th>Statically Typed (Rust, C, C++)</th>
      <th>Dynamically Typed (PHP, Python, JS)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Variable type</td>
      <td>Fixed once declared</td>
      <td>Can change at any time</td>
    </tr>
    <tr>
      <td>Type checking</td>
      <td>At compile time</td>
      <td>At execution time</td>
    </tr>
    <tr>
      <td>Performance</td>
      <td>Faster at runtime (no dynamic type checks)</td>
      <td>Slower (checks happen while running)</td>
    </tr>
    <tr>
      <td>Error detection</td>
      <td>Earlier (before running)</td>
      <td>Later (only when that line executes)</td>
    </tr>
  </tbody>
</table>

**PHP** — dynamic, reassigning a variable to a different type is fine:

```php
<?php
$num = 10;
$num = "Elzero";
echo $num;
```

**JavaScript** — no error until the offending line actually runs:

```js
let age = 30;

if (age > 30) {
  console.log("Good");
} else {
  console.log(age.repeat(3)); // only fails if this branch executes
}
```

**Python** — same idea, fails only at execution time:

```python
age = 30
if age > 30:
    print("Good")
else:
    print(age + "Bad")
```

**TypeScript** — catches the mismatch immediately, at compile time, even if that branch never runs:

```ts
let age = 40;
if (age > 30) {
  console.log("Good");
} else {
  console.log(age.repeat(3)); // error: Property 'repeat' does not exist on type 'number'
}
```

---

## Type Annotations (Signatures)

Type annotations indicate the data type of variables, and the input/output types of functions, objects, etc.

Questions worth keeping in mind as you go: Why do we use them? Are they mandatory? What happens if we skip them?

```ts
let theName = "Elzero";
let theAge: number = 40;
let hire: boolean = true;
let all: any = "Elzero Web School";
let allVars; // implicitly "any"

theName = "Osama";
all = 100;

function add(n1: number, n2: number) {
  return n1 + n2;
}

console.log(add(10, 20));
console.log(typeof add(10, 20));
```

Without annotations, JS silently coerces types you didn't intend:

```ts
function add(n1, n2) {
  return n1 + n2;
}

console.log(add(10, "20")); // "1020", string concatenation, not addition
console.log(typeof add(10, "20"));
```

### With Arrays

A union type restricts a variable to a fixed set of types:

```ts
let all: string | number | boolean = "Osama";

all = "A";
all = 100;
all = true;
```

A typed array only accepts elements of that type:

```ts
let myFriends: string[] = ["Osama", "Ahmed", "Sayed"];

for (let i = 0; i < myFriends.length; i++) {
  console.log(myFriends[i].repeat(3));
}
```

### With Multidimensional / Mixed Arrays

```ts
let arrayOne: number[] = [1, 2, 3, 4, 5];
let arrayTwo: string[] = ["A", "B", "C"];
let arrayThree: (string | number)[] = [1, 2, 3, 4, "A", "B", "C"];
let arrayFour: (string | number | string[] | boolean)[] =
  [1, 2, 3, 4, "A", "B", ["C", "D"], true, false];
```

### With Functions

Useful `tsconfig.json` compiler flags for functions:

|Flag|What it does|
|---|---|
|`noImplicitAny`|Without it, TypeScript silently allows implicit `any`|
|`noImplicitReturns`|Checks all code paths in a function return a value|
|`noUnusedLocals`|Errors on unused local variables|
|`noUnusedParameters`|Errors on unused function parameters|

```ts
let showMsg = true;

function showDetails(name: string, age: number, salary: number): string {
  let test = 10;
  if (showMsg) {
    return `Hello ${name}, Age Is ${age}, Salary Is ${salary}, Test Variable ${test}`;
  }
  return `No Data To Show`;
}

console.log(showDetails("Osama", 40, 5000));
```

### Optional and Default Parameters

In JavaScript every parameter is technically optional (it's just `undefined` if omitted). The `?` marks a parameter as optional in TypeScript:

```ts
function showData(name?: string, age?: number, country?: string) {
  return `${name} - ${age} - ${country}`;
}

console.log(showData("Osama", 40, "Egypt"));
```

A default value can stand in for a missing argument:

```ts
function showData(name = "Un", age, country) {
  return `${name} - ${age} - ${country}`;
}

console.log(showData(undefined, 40, "Egypt"));
```

### Rest Parameters

All numeric values — including floats — fall under the `number` type:

```ts
function addAll(...nums: number[]): number {
  let result = 0;
  for (let i = 0; i < nums.length; i++) {
    result += nums[i];
  }
  return result;
}

console.log(addAll(10, 20, 30, 100, 10.5, +true));
```

### Anonymous and Arrow Functions

```ts
const add = function (num1: number, num2: number): number {
  return num1 + num2;
};

console.log(add(10, 20));

const addWithArrow = (num1: number, num2: number): number => num1 + num2;

console.log(addWithArrow(10, 20));
```

> Solve: [[020_Notes/tracks/Fullstack/01-Frontend/26-Type Checkers/TypeScript Assignment|TypeScript Assignment Part 1]]

---

## Data Types

### Type Alias

A type alias gives a name to a type so you can reuse it:

```ts
type st = string;
let theName: st = "Elzero";
theName = "Osama";

type standnum = string | number;
let all: standnum = 10;
all = 100;
all = "Osama";
```

### Advanced Type Alias (Intersections)

`&` combines two object types into one shape:

```ts
type Buttons = {
  up: string;
  right: string;
  down: string;
  left: string;
};

type Last = Buttons & {
  x: boolean;
};

function getActions(btns: Last) {
  console.log(`Action For Button Up Is ${btns.up}`);
  console.log(`Action For Button Right Is ${btns.right}`);
  console.log(`Action For Button Down Is ${btns.down}`);
  console.log(`Action For Button Left Is ${btns.left}`);
}

getActions({ up: "Jump", right: "Go Right", down: "Go Down", left: "Go Left", x: true });
```

### Literal Types

Restricts a value to an exact, explicit set of literals rather than a whole type:

```ts
type nums = 0 | 1 | -1;

function compare(num1: number, num2: number): nums {
  if (num1 === num2) {
    return 0;
  } else if (num1 > num2) {
    return 1;
  } else {
    return -1;
  }
}

console.log(compare(20, 20)); // 0
console.log(compare(20, 15)); // 1
console.log(compare(20, 30)); // -1

let myNumber: nums = 1;
```

### Tuple

A tuple is an array with a fixed length and a known type at each position:

```ts
let article: readonly [number, string, boolean] = [11, "Title One", true];
article = [12, "Title Two", false];

const [id, title, published] = article;
console.log(id);
console.log(title);
console.log(published);
```

### Void and Never

`void` marks a function that returns nothing (note: `undefined` is not the same as `void`). `never` marks a function that never completes normally — it either throws or loops forever:

```ts
function logging(msg: string): void {
  console.log(msg);
  return;
}

console.log(logging("Iam A Message"));
console.log("Test");

const fail = (msg: string) => {
  throw new Error(msg);
};

function alwaysLog(name: string): never {
  while (true) {
    console.log(name);
  }
}

alwaysLog("Osama");
```

### Enums

An enum declares a set of named constants for logical grouping. By default, enums are number-based starting at `0`; they can also be string-based, or mixed ("heterogeneous").

Without an enum:

```ts
const KIDS = 15;
const EASY = 9;
const MEDIUM = 6;
const HARD = 3;
```

With an enum:

```ts
enum Level {
  Kids = 15,
  Easy = 9,
  Medium = 6,
  Hard = 3
}

let lvl: string = "Easy";

if (lvl === "Easy") {
  console.log(`The Level Is ${lvl} And Number Of Seconds Is ${Level.Easy}`);
}
```

Enums can reference other enums, reference themselves, run calculations, or call functions:

```ts
function getHardSeconds(): number {
  return 3;
}

enum Kids {
  Five = 25,
  Seven = 20,
  Ten = 15
}

enum Level {
  Kid = Kids.Ten,
  Easy = 9,
  Medium = Easy - 3,
  Hard = getHardSeconds()
}

let lvl: string = "Easy";

if (lvl === "Easy") {
  console.log(`The Level Is ${lvl} And Number Of Seconds Is ${Level.Hard}`);
}
```

### Type Assertions

Sometimes you know more about a value's type than the compiler does. TypeScript does **not** actually validate that the assertion is correct — it trusts you:

```ts
let myImg = <HTMLImageElement>document.getElementById("my-img");
// equivalent: let myImg = document.getElementById("my-img") as HTMLImageElement;
console.log(myImg.src);

let data: any = 1000;
console.log((data as string).repeat(3));
```

### Union and Intersection Types

Union (`|`) means "or"; intersection (`&`) means "and" — it combines several types into one:

```ts
type A = {
  one: string;
  two: number;
  three: boolean;
};

type B = A & {
  four: number;
};

type C = {
  five: boolean;
};

type mix = A & C;

function getActions(btns: mix) {
  console.log(`Hello ${btns.one}`);
  console.log(`Hello ${btns.two}`);
  console.log(`Hello ${btns.three}`);
  console.log(`Hello ${btns.five}`);
}

getActions({ one: "String", two: 100, three: true, five: true });
```

### With Objects

```ts
let myObject: {
  readonly username: string;
  id: number;
  hire?: boolean;
  skills: {
    one: string;
    two: string;
  };
} = {
  username: "Elzero",
  id: 100,
  hire: true,
  skills: {
    one: "HTML",
    two: "CSS"
  }
};

myObject.id = 101;
myObject.hire = false;

console.log(myObject.username);
console.log(myObject.id);
console.log(myObject.hire);
console.log(myObject.skills.one);
```

> Solve: [[020_Notes/tracks/Fullstack/01-Frontend/26-Type Checkers/TypeScript Assignment|TypeScript Assignment Part 2]]

---

## Interfaces

### Declaration

An interface describes the shape of an object — the syntax any matching object must follow. It can describe objects and function signatures, and supports `readonly` and optional (`?`) members:

```ts
interface User {
  id?: number;
  readonly username: string;
  country: string;
}

let user: User = {
  id: 100,
  username: "Elzero",
  country: "Egypt"
};

user.country = "Syria";

console.log(user);

function getData(data: User) {
  console.log(`Id Is ${data.id}`);
  console.log(`Username Is ${data.username}`);
  console.log(`Country Is ${data.country}`);
}

getData({ id: 200, username: "Osama", country: "KSA" });
```

### Methods and Parameters

```ts
interface User {
  id: number;
  username: string;
  country: string;
  sayHello(): string;
  sayWelcome: () => string;
  getDouble(num: number): number;
}

let user: User = {
  id: 100,
  username: "Elzero",
  country: "Egypt",
  sayHello() {
    return `Hello ${this.username}`;
  },
  sayWelcome: () => {
    return `Welcome ${user.username}`;
  },
  getDouble(n) {
    return n * 2;
  }
};

console.log(user.id);
console.log(user.sayHello());
console.log(user.sayWelcome());
console.log(user.getDouble(100));
```

### Reopening an Interface

Unlike a `type`, an interface with the same name declared multiple times gets merged — handy for progressively building up a shape across different parts of an app:

```ts
// Homepage
interface Settings {
  readonly theme: boolean;
  font: string;
}

// Articles Page
interface Settings {
  sidebar: boolean;
}

// Contact Page
interface Settings {
  external: boolean;
}

let userSettings: Settings = {
  theme: true,
  font: "Open Sans",
  sidebar: false,
  external: true
};
```

### Extending Interfaces

An interface can extend one or more other interfaces:

```ts
interface User {
  id: number;
  username: string;
  country: string;
}

interface Moderator {
  role: string | number;
}

interface Admin extends User, Moderator {
  protect?: boolean;
}

let user: Admin = {
  id: 100,
  username: "Elzero",
  country: "Egypt",
  role: "Mod",
  protect: true
};

console.log(user.id);
```

### Interface vs Type Alias

A common pattern: `HTMLElement` itself is an interface.

```ts
let el = document.getElementById("id") as HTMLElement;

type Settings = {
  readonly theme: boolean;
  font: string;
  sidebar: boolean;
  external: boolean;
};

let userSettings: Settings = {
  theme: true,
  font: "Open Sans",
  sidebar: false,
  external: true
};
```

---

## Classes

### Typing Class Members

```ts
class User {
  u: string;
  s: number;
  msg: () => string;

  constructor(username: string, salary: number) {
    this.u = username;
    this.s = salary;
    this.msg = function () {
      return `Hello ${this.u} Your Salary Is ${this.s}`;
    };
  }

  sayMsg() {
    return `Hello ${this.u} Your Salary Is ${this.s}`;
  }
}

let userOne = new User("Elzero", 6000);

console.log(userOne.u);
console.log(userOne.s);
console.log(userOne.msg());
console.log(userOne.sayMsg());
```

### Access Modifiers & Parameter Properties

|Modifier|Visibility|
|---|---|
|`public` (default)|Accessible anywhere, no restrictions|
|`private`|Only accessible inside the declaring class|
|`protected`|Like `private`, but also accessible from subclasses|

Remember: TypeScript is a layer on top of JavaScript. At compile time it strips out all annotations — including access modifiers like `private` — so these are compile-time-only guarantees, not runtime enforcement.

```ts
class User {
  msg: () => string;

  constructor(private username: string, protected salary: number, public readonly address: string) {
    this.msg = function () {
      return `Hello ${this.username} Your Salary Is ${this.salary}`;
    };
  }

  sayMsg() {
    return `Hello ${this.username} Your Salary Is ${this.salary}`;
  }
}

let userOne = new User("Elzero", 6000, "Cairo");

console.log(userOne.msg());
console.log(userOne.sayMsg());
```

### Get and Set Accessors

```ts
class User {
  public get username(): string {
    return this._username;
  }

  public set username(value: string) {
    this._username = value;
  }

  msg: () => string;

  constructor(private _username: string, public salary: number, public readonly address: string) {
    this.msg = function () {
      return `Hello ${this._username} Your Salary Is ${this.salary}`;
    };
  }

  sayMsg() {
    return `Hello ${this._username} Your Salary Is ${this.salary}`;
  }
}

let userOne = new User("Elzero", 6000, "Cairo");

console.log(userOne.username);
userOne.username = "Ahmed";
console.log(userOne.username);
console.log(userOne.salary);
console.log(userOne.msg());
console.log(userOne.sayMsg());
```

### Static Members

Note: avoid naming static members `name`, `length`, or `call` — they collide with built-in `Function` properties.

```ts
class User {
  private static created: number = 0;

  static getCount(): void {
    console.log(`${this.created} Objects Created`);
  }

  constructor(public username: string) {
    User.created++;
  }
}

let u1 = new User("Elzero");
let u2 = new User("Web");
let u3 = new User("School");

User.getCount();
```

### Implementing an Interface

```ts
interface Settings {
  theme: boolean;
  font: string;
  save(): void;
}

class User implements Settings {
  constructor(public username: string, public theme: boolean, public font: string) {}

  save(): void {
    console.log(`Saved`);
  }

  update(): void {
    console.log(`Updated`);
  }
}

let userOne = new User("Elzero", true, "Open Sans");

console.log(userOne.username);
console.log(userOne.font);

userOne.save();
userOne.update();
```

> Solve: [[020_Notes/tracks/Fullstack/01-Frontend/26-Type Checkers/TypeScript Assignment|TypeScript Assignment Part 3]]

---

## Abstract Classes and Members

An abstract class cannot be instantiated directly — it exists to be extended:

```ts
abstract class Food {
  constructor(public title: string) {}
  abstract getCookingTime(): void;
}

class Pizza extends Food {
  constructor(title: string, public price: number) {
    super(title);
  }
  getCookingTime(): void {
    console.log(`Cooking Time For Pizza Is 1 Hour`);
  }
}

class Burger extends Food {
  constructor(title: string, public price: number) {
    super(title);
  }
  getCookingTime(): void {
    console.log(`Cooking Time For Burger Is Half Hour`);
  }
}

let pizzaOne = new Pizza("Awesome Pizza", 100);

console.log(pizzaOne.title);
console.log(pizzaOne.price);
pizzaOne.getCookingTime();
```

## Polymorphism & Method Override

- **Polymorphism**: classes share the same method name but each implements it differently.
- **Method override**: a child class provides its own implementation of a method already defined in the parent; the method name must match exactly. The `override` keyword (paired with the `noImplicitOverride` compiler flag) makes this explicit and safer.

```ts
class Player {
  constructor(public name: string) {}
  attack(): void {
    console.log("Attacking Now");
  }
}

class Amazon extends Player {
  constructor(name: string, public spears: number) {
    super(name);
  }
  override attack(): void {
    console.log("Attacking With Spear");
    this.spears -= 1;
  }
}

class Barbarian extends Player {
  constructor(name: string, public axeDurability: number) {
    super(name);
  }
  override attack(): void {
    console.log("Attacking With Axe");
    this.axeDurability -= 1;
  }
}

let barOne = new Barbarian("Elzero", 100);

console.log(barOne.name);
barOne.attack();
console.log(barOne.axeDurability);
```

---

## Generics

Generics let you write reusable code by passing a _type_ as a parameter to another type — so you can support multiple types without falling back to `any`. TypeScript supports generic functions, methods, classes, and interfaces.

The problem generics solve — repeating the same function per type:

```ts
function returnNumber(val: number): number {
  return val;
}
function returnString(val: string): string {
  return val;
}
function returnBoolean(val: boolean): boolean {
  return val;
}

console.log(returnNumber(100));
console.log(returnString("Elzero"));
console.log(returnBoolean(true));
```

One generic function instead:

```ts
function returnType<T>(val: T): T {
  return val;
}

console.log(returnType<number>(100));
console.log(returnType<string>("Elzero"));
console.log(returnType<boolean>(true));
console.log(returnType<number[]>([1, 2, 3, 4]));
```

### Arrow Syntax and Multiple Type Parameters

```ts
const returnTypeArrowSyntax = <T>(val: T): T => val;

console.log(returnTypeArrowSyntax<number>(100));
console.log(returnTypeArrowSyntax<string>("Elzero"));

function testType<T>(val: T): string {
  return `The Value Is ${val} And Type Is ${typeof val}`;
}

console.log(testType<number>(100));
console.log(testType<string>("Elzero"));

function multipleTypes<T, S>(valueOne: T, valueTwo: S): string {
  return `The First Value Is ${valueOne} And Second Value ${valueTwo}`;
}

console.log(multipleTypes<string, number>("Osama", 100));
console.log(multipleTypes<string, boolean>("Elzero", true));
```

### Generic Classes

```ts
class User<T = string> {
  constructor(public value: T) {}
  show(msg: T): void {
    console.log(`${msg} - ${this.value}`);
  }
}

let userOne = new User<string>("Elzero");
console.log(userOne.value);
userOne.show("Message");

let userTwo = new User<number | string>(100);
console.log(userTwo.value);
userTwo.show("Message");
```

### Generic Classes with Interfaces

```ts
interface Book {
  itemType: string;
  title: string;
  isbn: number;
}

interface Game {
  itemType: string;
  title: string;
  style: string;
  price: number;
}

class Collection<T> {
  public data: T[] = [];
  add(item: T): void {
    this.data.push(item);
  }
}

let itemOne = new Collection<Book>();
itemOne.add({ itemType: "Book", title: "Atomic Habits", isbn: 150510 });
itemOne.add({ itemType: "Book", title: "Follow Your Heart", isbn: 650650 });
console.log(itemOne);

let itemTwo = new Collection<Game>();
itemTwo.add({ itemType: "Game", title: "Uncharted", style: "Action", price: 150 });
console.log(itemTwo);
```

> Solve: [[020_Notes/tracks/Fullstack/01-Frontend/26-Type Checkers/TypeScript Assignment|TypeScript Assignment Part 4]]

---

## How to Continue

- Practice
- Explore topics not covered in the course
- JSDoc
- Deeper `tsconfig.json` options