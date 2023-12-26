
You can combine logical expressions to create increasingly cleverer and more useful checks. One good example is password verification. As you know, some websites want a password of 8 to 20 characters on signup. Frankly, it's a weird restriction, but whatever, it is what it is. In math, we would write `8 < x < 20` (where `x` is the length of a particular password), but that trick won't work in JavaScript.  We would have to make two separate logical expressions and connect them with the special "AND" operator:

```
A password longer than 8 characters **AND** a password shorter than 20 characters.
```

Here's a function that takes the password and says whether it meets the conditions or not:

```javascript
const isStrongPassword = (password) => {
  const length = password.length;
  return length > 8 && length < 20;
};

isStrongPassword('qwerty'); // false
isStrongPassword('qwerty1234'); // true
isStrongPassword('zxcvbnmasdfghjkqwertyui'); // false
```

`&&` means "AND" (called a conjunction in mathematical logic). The whole expression is true only when every operand, which are all part of the compound expressions, is true. In other words, `&&` means "both".

This operator's priority is lower than that of comparison operators, so the expression works correctly without parentheses.

Another widespread operator along with `&&` is `||` — "OR" (disjunction). It means "one or the other, or both". Operators can be combined in any number and any sequence, but when `&&` and `||` appear together, you should label priority with parentheses. Below is an example of an advanced function validating a password:

```javascript
const hasSpecialChars = (str) => /* checks for special characters in the string */;

const isStrongPassword = (password) => {
  const length = password.length;
  // The parentheses set the priority, making it clear how each part is related
  return (length > 8 && length < 20) || hasSpecialChars(password);
};
```

Another example. We want to buy an apartment that meets these conditions: an area of 100 square meters or more on any street **OR** an area of 80 square meters or more, but on `Main Street`.

We'll write a function checking the apartment. It takes two arguments: the area (a number) and the street name (a string):

```javascript
const isGoodApartment = (area, street) => {
  // Via a variable to make sure the function is not too long
  const result = area >= 100 || (area >= 80 && street === 'Main Street');
  return result;
};

isGoodApartment(91, 'Queens Street'); // false
isGoodApartment(78, 'Queens Street'); // false
isGoodApartment(70, 'Main Street');   // false

isGoodApartment(120, 'Queens Street'); // true
isGoodApartment(120, 'Main Street');   // true
isGoodApartment(80, 'Main Street');    // true
```

The area of mathematics dealing with logical operators is called Boolean algebra. The "truth tables" are shown below and can be used to figure out the result of an operator:

## AND `&&`

| A     | B     | A && B   |
|-------| ------|----------|
| TRUE  | TRUE  | **TRUE** |
| TRUE  | FALSE | FALSE    |
| FALSE | TRUE  | FALSE    |
| FALSE | FALSE | FALSE    |

Few examples:

```javascript
// true && true;
3 > 2 && 'wow'.startsWith('w'); // true

// true && false;
'start' === 'start' && 8 < 3; // false
```

## OR `||`

| A     | B     | A &vert;&vert; B |
|-------|-------|----------|
| TRUE  | TRUE  | **TRUE** |
| TRUE  | FALSE | **TRUE** |
| FALSE | TRUE  | **TRUE** |
| FALSE | FALSE | FALSE    |

Few examples:

```javascript
// true || true;
3 > 2 || 'wow'.startsWith('w'); // true

// false || false;
'start' === 'Start' || 3 < 3; // false
```
