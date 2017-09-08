# Exploring ES6

## Data

## Symbols
- a new primitive type
- new instance every time
- they are all unique
```javascript
const mySymbol = Symbol('mySymbol');
```



### Use case 1: unique property keys
- they can be iterable using `Symbol.iterator`




### Use case 2: constants representing concepts
```javascript
const COLOR_RED    = Symbol('Red');
const COLOR_ORANGE = Symbol('Orange');

function getComplement(color) {
    switch (color) {
        case COLOR_RED:
            return COLOR_GREEN;
        case COLOR_ORANGE:
            return COLOR_BLUE;
        default:
            throw new Exception('Unknown color: '+color);
    }
}
```



#### Pitfall: you can’t coerce symbols to strings
```javascript
const sym = Symbol('desc');

const str1 = '' + sym; // TypeError
const str2 = `${sym}`; // TypeError

const str2 = String(sym); // 'Symbol(desc)'
const str3 = sym.toString(); // 'Symbol(desc)'
```



#### Which operations related to property keys are aware of symbols?
- The following operations are aware of symbols as property keys:
    - Reflect.ownKeys()
    - Property access via []
    - Object.assign()
  
- The following operations ignore symbols as property keys:
    - Object.keys()
    - Object.getOwnPropertyNames()
    - for-in loop




### A new primitive type
- They are tokens that serve as unique IDs
- You create symbols via the factory function `Symbol()`
```javascript
const symbol1 = Symbol();
```

- converting to string will give different result
```javascript
const symbol2 = Symbol('symbol2');
String(symbol2)
'Symbol(symbol2)'
```

- every symbol is unique
```javascript
Symbol() === Symbol()
false
```

- `typeof` will show its type
```javascript
typeof Symbol()
'symbol'
```


#### Symbols as property keys
```javascript
const MY_KEY = Symbol();
const obj = {};

obj[MY_KEY] = 123;
console.log(obj[MY_KEY]); // 123
```

- symbols can be used as object keys, but they need tho be in brackets
```javascript
const MY_KEY = Symbol();
const obj = {
    [MY_KEY]: 123
};

const FOO = Symbol();
const obj = {
    [FOO]() {
        return 'bar';
    }
};
console.log(obj[FOO]()); // bar
``` 



#### Enumerating own property keys
- Property keys are either strings or symbols.
- String-valued property keys are called property names.
- Symbol-valued property keys are called property symbols.




### Symbols as keys of properties




#### Symbols as keys of non-public properties
- Public properties are seen by clients of the code
- Private properties are used within classes/mixins
```javascript
const _counter = Symbol('counter');
const _action = Symbol('action');
class Countdown {
    constructor(counter, action) {
        this[_counter] = counter;
        this[_action] = action;
    }
    dec() {
        let counter = this[_counter];
        if (counter < 1) return;
        counter--;
        this[_counter] = counter;
        if (counter === 0) {
            this[_action]();
        }
    }
}
```
