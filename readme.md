# Exploring ES6

## Data

## New string features


### Overview
```angular2html
'hello'.startsWith('hell')
true

'hello'.endsWith('ello')
true

'hello'.includes('ell')
true

'doo '.repeat(3)
'doo doo doo '

// String interpolation via template literals (in backticks)
const first = 'Jane';
const last = 'Doe';
console.log(`Hello ${first} ${last}!`);
    // Hello Jane Doe!

// Template literals also let you create strings with multiple lines
const multiLine = `
This is
a string
with multiple
lines`;
```


### String interpolation, multi-line string literals and raw string literals
- `String.raw`
```angular2html
const str = String.raw`Not a newline: \n`;
console.log(str === 'Not a newline: \\n'); // true
```



### Iterating over strings
- Strings are iterable, so we can use `for-of`
```angular2html
for (const ch of 'abc') {
    console.log(ch);
}
// Output:
// a
// b
// c
```

- operator `(...)` can be used to convert string to array
```angular2html
const chars = [...'abc'];
    // ['a', 'b', 'c']
```



### Checking for inclusion
- has optional second parameter, which specifies where the string to be searched starts or ends
```angular2html
> 'hello'.startsWith('ello', 1)
true
> 'hello'.endsWith('hell', 4)
true

> 'hello'.includes('ell', 1)
true
> 'hello'.includes('ell', 2)
false
```