---
label: JS and TS
---

## TS stuff

### Types and interfaces
```
type User = {
    name: string
}

interface User {
    name: string
}
```

- Interfaces are made to represent objects and DTOs.
- Types are made to make few types work as close as primative types, but it can go as complex as you need.
- Interfaces can only be used to define type of object, type can be used for single type e.g. `type SType = string | number`
- Types can use union of multiple types

```
type SType = { name: string } | { age: number}
type SType = { name: string } & { age: number}
const user: Stype = { name: 'string' }
```

### Use unknown instead of any
- `unknown` is the union of every type there is.
- `any` is the "elastic" type which fits to what it needs to be. (It may also be thought of as the switch to selectively disable type checking)

```
interface IUser {
    name: string
}

interface IAdminUser extends IUser {
    token: string;
    addNewUser: () => void;
}

// typeguard
function isAdminUser(object: unknown): object is IAdminUser {
    if (object !== null && typeof object === "object") {
        return "token" in object;
    }
    return false;
}

async function fetchUser() {
    const res = await fetch("someurl");

    const user: unknown = await res.json();
    if (isAdminUser()) {
        // then we know the type here
    }
}
```

### is Operator
```
type Species = 'cat' | 'dog';
interface Pet {
    species: Species;
}

class Cat implements Pet {
    public species: Species = 'cat';
    public meow(): void {
        console.log('meow');
    }
}
function petIsCat(pet: Pet): pet is Cat {
    return pet.species === 'cat';
}
const p: Pet = new Cat();

if (petIsCat(p)) {
    p.meow(); // can access
}

// type cast
(p as Cat).meow();
```

### satisfies
To match some type for inference purposes.
```
type UserImage = string | ICustomImage;

const user = {
    id: 1,
    image: "image-url"
} satisfies IUser;
```

### Enums
```
type State = "InProgress" | "Success" | "Fail"
or
enum State {
    InProgress = "InProgress"
    Success = "Success"
    Fail = "Fail"
} // do not use numbers
cosnt checkState = (state: State) => {};
```

### Utility
```
// to avoid having to create another interface to make fields optional when you only want to update a few fields
function updateProduct() {
    productId: IProduct["id"],
    updatedProduct: Partial<Omit<IProduct, "id">>   
} {}

// record
type Properties = "red" | "green" | "blue";
type RGB = [red: number, green: number, blue" number];
const color: Record<Properties, RGB | string> = {
    red: [255, 0, 0],
    green: 'green',
    blue: 'blue'
};
```

## JS stuff

### Arrow functions
```
const myFnc = () = {
    ...
}
```
No more issues with the `this` keyword!

### Exports and Imports
#### Default export
```
import person from './person.js'
```

#### Named export
```
import { smth } from './utility.js'
import * as bundled from './utility.js'
```

### Classes
Classes are a feature which basically replace constructor functions and prototypes. You can define blueprints for JavaScript objects with them. 
```
class Human {
    constructor() {
        this.gender = 'male';
    }
}
class Person extends Human {
    constructor() {
        super();
        this.name = 'test';
    }
}
const person = new Person();
```

### Spread/Rest operators
Spread is used to split up array elements or object properties
```
const arr = [...oldArr, 1, 2]
const newObj = {...oldObj, newProp: 5}
```

Rest is used to merge a list of function arguments into an array
```
function sortArgs(...args) {
    return args.sort()
}
```

### Destructing
Easily extract array elements or object properties and store them in variables
```
[a, b] = ['Hello', 'World']
{name} = {name: 'Name', age: 1}
```

### Reference and primitive types
Objects and arrays are reference types (just copy the pointer)

Use spread operator to copy.
```
const secondPerson = {
    ...person
}
```

### Arrow functions
An arrow function expression is a compact alternative to a traditional function expression, with some semantic differences and deliberate limitations in usage:

- Arrow functions don't have their own bindings to this, arguments, or super, and should not be used as methods.
- Arrow functions cannot be used as constructors. Calling them with new throws a TypeError. They also don't have access to the new.target keyword.
- Arrow functions cannot use yield within their body and cannot be created as generator functions.

```Syntax
param => expression

(param) => expression

(param1, paramN) => expression

param => {
  statements
}

(param1, paramN) => {
  statements
}
```

## References
- https://www.youtube.com/watch?v=ZCllX1p763U