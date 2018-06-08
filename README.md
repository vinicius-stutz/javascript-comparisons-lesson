# Javascript Comparisons
Does it matter which equals operator (== vs. ===) I use in JavaScript comparisons?

The identity (`===`) operator behaves identically to the equality (`==`) operator except no type conversion is done, and the types must be the same to be considered equal.

Reference:  [Javascript Tutorial: Comparison Operators](http://www.c-point.com/javascript_tutorial/jsgrpComparison.htm)

The  `==`  operator will compare for equality  _after doing any necessary type conversions_. The  `===`  operator will  **not**  do the conversion, so if two values are not the same type  `===`  will simply return  `false`. It's this case where  `===`  will be faster, and may return a different result than  `==`. In all other cases performance will be the same.

To quote Douglas Crockford's excellent  [JavaScript: The Good Parts](http://rads.stackoverflow.com/amzn/click/0596517742),

> JavaScript has two sets of equality operators:  `===`  and  `!==`, and their evil twins  `==`  and  `!=`. The good ones work the way you would expect. If the two operands are of the same type and have the same value, then  `===`  produces  `true`  and  `!==`  produces  `false`. The evil twins do the right thing when the operands are of the same type, but if they are of different types, they attempt to coerce the values. the rules by which they do that are complicated and unmemorable. These are some of the interesting cases:
> 
> ```
> '' == '0'           // false
> 0 == ''             // true
> 0 == '0'            // true
> 
> false == 'false'    // false
> false == '0'        // true
> 
> false == undefined  // false
> false == null       // false
> null == undefined   // true
> 
> ' \t\r\n ' == 0     // true
> ```
> 
> The lack of transitivity is alarming. My advice is to never use the evil twins. Instead, always use  `===`  and  `!==`. All of the comparisons just shown produce  `false`  with the  `===`  operator.

----------

### Update:

A good point was brought up by  [@Casebash](http://stackoverflow.com/users/165495/casebash)  in the comments and in  [@Phillipe Laybaert's](http://stackoverflow.com/users/113570/philippe-leybaert)  [answer](http://stackoverflow.com/a/957602/1288)  concerning reference types. For reference types  `==`  and  `===`  act consistently with one another (except in a special case).

```
var a = [1,2,3];
var b = [1,2,3];

var c = { x: 1, y: 2 };
var d = { x: 1, y: 2 };

var e = "text";
var f = "te" + "xt";

a == b            // false
a === b           // false

c == d            // false
c === d           // false

e == f            // true
e === f           // true
```

The special case is when you compare a literal with an object that evaluates to the same literal, due to its  `toString`  or  `valueOf`  method. For example, consider the comparison of a string literal with a string object created by the  `String`  constructor.

```
"abc" == new String("abc")    // true
"abc" === new String("abc")   // false
```

Here the  `==`  operator is checking the values of the two objects and returning  `true`, but the  `===`  is seeing that they're not the same type and returning  `false`. Which one is correct? That really depends on what you're trying to compare. My advice is to bypass the question entirely and just don't use the  `String`  constructor to create string objects.

**Reference**  
[http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3](http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3)
