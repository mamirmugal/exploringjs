# Exploring ES6

## Data

## New number and Math features


### Overview



#### New integer literals
```angular2html
0xFF // ES5: hexadecimal
255

0b11 // ES6: binary
3

0o10 // ES6: octal
8
```



#### New Number properties
- `Number.isInteger(num)`, checks whether `num` is an integer, but without fraction
```angular2html
Number.isInteger(1.05)
false
Number.isInteger(1)
true

Number.isInteger(-3.1)
false
Number.isInteger(-3)
true
``` 

- `Number.isNaN(num)`, checks if `num` is `NaN`
```angular2html
isNaN('???')
true

Number.isNaN('???')
false
```



#### New Math methods
- `Math.sign()` returns the sign of a number
```angular2html
Math.sign(-8)
-1

Math.sign(0)
0

Math.sign(3)
1
```

- `Math.trunc()` removes the decimal fraction of a number
```angular2html
Math.trunc(3.1)
3

Math.trunc(3.9)
3

Math.trunc(-3.1)
-3

Math.trunc(-3.9)
-3
```



### New integer literals
- method `toString(radix)` can be used to see numbers in a base other than 10
```angular2html
255..toString(16)
'ff'

4..toString(2)
'100'

8..toString(8)
'10'
```



### New static Number properties
- methods: `isFinite` and `isNaN`, `parseFloat` and `parseInt`
- they are properties of `Number` 
- they are also available as global functions
- `isFinite` and `isNaN` are dont work the same



#### Number.isFinite(number)
- it determines if the `number` is an actual number
```angular2html
Number.isFinite(Infinity)
false

Number.isFinite(-Infinity)
false

Number.isFinite(NaN)
false

Number.isFinite(123)
true

------------------------------------

Number.isFinite('123')
false

isFinite('123')
true
```



#### Number.isNaN(number)
- with global
```angular2html
isNaN('???')
true
```

- but with number wrapper
```angular2html
Number.isNaN('???')
false
```



#### Number.isInteger(number) 
```angular2html
Number.isInteger(-17)
true

Number.isInteger(33)
true

Number.isInteger(33.1)
false

Number.isInteger('33')
false

Number.isInteger(NaN)
false

Number.isInteger(Infinity)
false
```



### New Math functionality



#### Various numerical functionality
- `Math.sign(x)` returns
    - -1 if x is a negative number (including -Infinity).
    - 0 if x is zero.
    - +1 if x is a positive number (including Infinity).
    - NaN if x is NaN or not a number
    
```angular2html
Math.sign(-8)
-1
Math.sign(3)
1

Math.sign(0)
0
Math.sign(NaN)
NaN

Math.sign(-Infinity)
-1
Math.sign(Infinity)
1
```

- `Math.trunc(x)`, removes decimal places
```angular2html
Math.trunc(3.1)
3

Math.trunc(3.9)
3

Math.trunc(-3.1)
-3

Math.trunc(-3.9)
-3
```



#### Support for compiling to JavaScript
- `Math.fround(x)`, rounds x to a 32 bit floating point value (float)
    