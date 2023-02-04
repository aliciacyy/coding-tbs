---
label: Javascript
---

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
