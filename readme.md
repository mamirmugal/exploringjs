# Exploring ES6

## Background

## Core ES6 features


### From var to const/let
- `var` has problems when not defined in particular scope
- if a value is declared but not assigned it will still return as `undefined`
```angular2html
var x = 3;
function func(randomize) {
    var x;
    if (randomize) {
        x = Math.random();
        return x;
    }
    return x;
}
func(false); // undefined
```
- but with `let` engine can figure out the variable with scope and pick which is accessible
```angular2html
let x = 3;
function func(randomize) {
    if (randomize) {
        let x = Math.random();
        return x;
    }
    return x;
}
func(false); // 3
```

- use `const` for value who's value are not changed 
- use `let` for everything else



### From IIFEs to blocks
- in ES5 we need to use IIFE for variable scope restriction
```angular2html
(function () {  // open IIFE
    var tmp = ···;
    ···
}());  // close IIFE

console.log(tmp); // ReferenceError
```

- but in ES6 we can use just `blocks`
```angular2html
{  // open block
    let tmp = ···;
    ···
}  // close block

console.log(tmp); // ReferenceError
```


### From concatenating strings to template literals 



#### String interpolation 
- in ES5 we need concat variables with string but in ES6 we can use them in strings
```angular2html
function printCoord(x, y) {
    console.log(`(${x}, ${y})`);
}
``` 



#### Multi-line strings 
- ES5 don't support multiple lines strings, without escape 
- but ES6 does
```angular2html
const HTML5_SKELETON = `
    <!doctype html>
    <html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
    </body>
    </html>`;
```



### From function expressions to arrow functions
- in ES5 we need to assign `this` to variable from getting shadowed
```angular2html
function UiComponent() {
    var _this = this; // (A)
    var button = document.getElementById('myButton');
    button.addEventListener('click', function () {
        _this.handleClick(); // (B)
    });
}
```

- but in ES6 we can use arrow function, which dont shadow variables
```angular2html
function UiComponent() {
    var button = document.getElementById('myButton');
    button.addEventListener('click', () => {
        this.handleClick(); // (A)
    });
}
```

- arrow functions are also helpful in short callbacks with only return values
```angular2html
var arr = [1, 2, 3];
var squares = arr.map(function (x) { return x * x });

// to

const arr = [1, 2, 3];
const squares = arr.map(x => x * x); // parenthesis can be omitted with one param
```



### Handling multiple return values 



#### Multiple return values via arrays
```angular2html
const cal = function() { return [1,2,3] };

const [one, two, three] = cal();

one
1
```



### Multiple return values via objects
- properties of object are translated to object properties
```angular2html
const obj = { foo: 123 };

const {writable, configurable} =
    Object.getOwnPropertyDescriptor(obj, 'foo');

console.log(writable, configurable); // true true

-----------------------------------------------------------

const cal = function() { 
    return { 
        a:1,
        b:2,
        c:3
    }; 
};

const {a, c} = cal();

c
3
```


### From for to forEach() to for-of
```angular2html
const arr = ['a', 'b', 'c'];
for (const elem of arr) {
    console.log(elem);
}
```

- `entries()` method can be used to get value and index of an array
```angular2html
for (const [index, elem] of arr.entries()) {
    console.log(index+'. '+elem);
}
```



### Handling parameter default values
- same as php language 
```angular2html
function foo(x=0, y=0) {
    ···
}
```



### Handling named parameters
- in ES5 
```angular2html
function selectEntries(options) {
    var start = options.start || 0;
    var end = options.end || -1;
    var step = options.step || 1;
    ···
}
```

- in ES6, default value can be assigned 
```angular2html
function selectEntries({ start=0, end=-1, step=1 }) {
    console.log(start)
}

```



#### Making the parameter optional 
```angular2html
function selectEntries({ start=0, end=-1, step=1 } = {}) {
    ···
}
```



### From arguments to rest parameters
- `...` can be used followed by any variable name
```angular2html
function logAllArguments(...args) {
    for (const arg of args) {
        console.log(arg);
    }
}

logAllArguments(1,2)
2
```

- param can also be used with them
```angular2html
function logAllArguments(val, ...args) {
    for (const arg of args) {
        console.log(arg);
    }
}

logAllArguments(1,2)
2
```



### From apply() to the spread operator (...) 
- `apply` method need a specific obj, usually its own object of `this`



#### Math.max()
- in ES5
```angular2html
Math.max.apply(Math, [-1, 5, 11, 3])
11
```

- in ES6 
```angular2html
Math.max(...[-1, 5, 11, 3])
11
```



#### Array.prototype.push()
- in ES5
```angular2html
var arr1 = ['a', 'b'];
var arr2 = ['c', 'd'];

arr1.push.apply(arr1, arr2);
// arr1 is now ['a', 'b', 'c', 'd']
```

- in ES6 
```angular2html
const arr1 = ['a', 'b'];
const arr2 = ['c', 'd'];

arr1.push(...arr2);
// arr1 is now ['a', 'b', 'c', 'd']
```



### From concat() to the spread operator (...)
- in ES5
```angular2html
var arr1 = ['a', 'b'];
var arr2 = ['c'];
var arr3 = ['d', 'e'];

console.log(arr1.concat(arr2, arr3));
    // [ 'a', 'b', 'c', 'd', 'e' ]
```

- in ES6
```angular2html
const arr1 = ['a', 'b'];
const arr2 = ['c'];
const arr3 = ['d', 'e'];

console.log([...arr1, ...arr2, ...arr3]);
    // [ 'a', 'b', 'c', 'd', 'e' ]
```


### From function expressions in object literals to method definitions
- in ES5
```angular2html
var obj = {
    foo: function () {
        ···
    },
    bar: function () {
        this.foo();
    }, // trailing comma is legal in ES5
}
```

- in ES6
```angular2html
const obj = {
    foo() {
        ···
    },
    bar() {
        this.foo();
    },
}
```


### From constructors to classes



#### Base classes
- in ES5
```angular2html
function Person(name) {
    this.name = name;
}
Person.prototype.describe = function () {
    return 'Person called '+this.name;
};
```

- in ES6
- there are no commas between functions
- there are keyword `function` before methods
```angular2html
class Person {
    constructor(name) {
        this.name = name;
    }
    describe() {
        return 'Person called '+this.name;
    }
}
```


#### Derived classes
- in ES5
```angular2html
function Employee(name, title) {
    Person.call(this, name); // super(name)
    this.title = title;
}
Employee.prototype = Object.create(Person.prototype);
Employee.prototype.constructor = Employee;
Employee.prototype.describe = function () {
    return Person.prototype.describe.call(this) // super.describe()
           + ' (' + this.title + ')';
};
```

- ES6, has built in support for subclassing, with keyword `extends`
```angular2html
class Employee extends Person {
    constructor(name, title) {
        super(name);
        this.title = title;
    }
    describe() {
        return super.describe() + ' (' + this.title + ')';
    }
}
```



### From custom error constructors to subclasses of Error
- in ES5, handling exceptions was difficult
- in ES6, it is easy
```angular2html
class MyError extends Error {

}
```


### From objects to Maps 
```angular2html
const map = new Map();
function countWords(word) {
    const count = map.get(word) || 0;
    map.set(word, count + 1);
}
```


### New string methods
- `From indexOf to startsWith`
```angular2html
if (str.indexOf('x') === 0) {} // ES5
if (str.startsWith('x')) {} // ES6
```

- `From indexOf to endsWith`
```angular2html
function endsWith(str, suffix) { // ES5
  var index = str.indexOf(suffix);
  return index >= 0
    && index === str.length-suffix.length;
}
str.endsWith(suffix); // ES6
```

- `From indexOf to includes`
```angular2html
if (str.indexOf('x') >= 0) {} // ES5
if (str.includes('x')) {} // ES6
```

- `From join to repeat`
```angular2html
new Array(3+1).join('#') // ES5
'#'.repeat(3) // ES6

```



### New Array methods



#### From Array.prototype.indexOf to Array.prototype.findIndex
```angular2html
const arr = ['a', NaN];

arr.indexOf(NaN); // -1
arr.findIndex(x => Number.isNaN(x)); // 1
```



#### From Array.prototype.slice() to Array.from() or the spread operator
```angular2html
var arr1 = Array.prototype.slice.call(arguments); // ES5
const arr2 = Array.from(arguments); // ES6
```



#### From apply() to Array.prototype.fill()
```angular2html
// Same as Array(undefined, undefined)
var arr1 = Array.apply(null, new Array(2));     // [undefined, undefined]
const arr2 = new Array(2).fill(undefined);    // [undefined, undefined]
```



### From CommonJS modules to ES6 modules
- ES6 has built-in support for modules
- but, no js engine supports them natively, yet
- But tools such as browserify, webpack let you use ES6 syntax to create modules



#### Multiple exports


##### Multiple exports in CommonJS
- In CommonJS, you export multiple entities as follows
```angular2html
//------ lib.js ------
var sqrt = Math.sqrt;
function square(x) {
    return x * x;
}
function diag(x, y) {
    return sqrt(square(x) + square(y));
}
module.exports = {
    sqrt: sqrt,
    square: square,
    diag: diag,
};

//------ main1.js ------
var square = require('lib').square;
var diag = require('lib').diag;

console.log(square(11)); // 121
console.log(diag(4, 3)); // 5

//------ main2.js ------
var lib = require('lib');
console.log(lib.square(11)); // 121
console.log(lib.diag(4, 3)); // 5
```



##### Multiple exports in ES6
```angular2html
//------ lib.js ------
export const sqrt = Math.sqrt;
export function square(x) {
    return x * x;
}
export function diag(x, y) {
    return sqrt(square(x) + square(y));
}

//------ main1.js ------
import { square, diag } from 'lib';
console.log(square(11)); // 121
console.log(diag(4, 3)); // 5
The syntax for importing modules as objects looks as follows (line A):

//------ main2.js ------
import * as lib from 'lib'; // (A)
console.log(lib.square(11)); // 121
console.log(lib.diag(4, 3)); // 5
```



#### Single exports



##### Single exports in CommonJS
```angular2html
//------ myFunc.js ------
module.exports = function () { ··· };

//------ main1.js ------
var myFunc = require('myFunc');
myFunc();
```



##### Single exports in ES6
```angular2html
//------ myFunc.js ------
export default function () { ··· } // no semicolon!

//------ main1.js ------
import myFunc from 'myFunc';
myFunc();
```