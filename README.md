
[<img src="https://github-ads.s3.eu-central-1.amazonaws.com/support-ukraine.svg?t=1" />](https://supportukrainenow.org)

# JavaScript Style Guide

A work in progress JavaScript style guide for our projects at [Spatie](https://spatie.be).

Spatie is a webdesign agency in Antwerp, Belgium. You'll find an overview of all our open source projects [on our website](https://spatie.be/opensource).

## Support us

[<img src="https://github-ads.s3.eu-central-1.amazonaws.com/javascript-styleguide.jpg?t=1" width="419px" />](https://spatie.be/github-ad-click/javascript-styleguide)

We invest a lot of resources into creating [best in class open source packages](https://spatie.be/open-source). You can support us by [buying one of our paid products](https://spatie.be/open-source/support-us).

We highly appreciate you sending us a postcard from your hometown, mentioning which of our package(s) you are using. You'll find our address on [our contact page](https://spatie.be/about-us). We publish all received postcards on [our virtual postcard wall](https://spatie.be/open-source/postcards).

## ESLint

This guide should be used side by side with our base ESLint configuration file, which has it's own repository and is available on npm.

https://github.com/spatie/eslint-config-spatie

```
yarn add --dev eslint-config-spatie
```

## Code Style

- [Spacing and Indentation in Functions and Control Statements](#spacing-and-indentation-in-functions-and-control-statements)
- [Spacing and Indentation in Objects and Arrays](#spacing-and-indentation-in-objects-and-arrays)
- [Line Length](#line-length)
- [Quotes](#quotes)
- [Semicolons](#semicolons)
- [Variable Assignment](#variable-assignment)
- [Variable Names](#variable-names)
- [Comparisons](#comperisons)
- [Function Keyword vs. Arrow Functions](#function-keyword-vs-arrow-functions)
- [Arrow Function Parameter Brackets](#arrow-function-parameter-brackets)
- [Object and Array Destructuring](#object-and-array-destructuring)

### Spacing and Indentation in Functions and Control Statements

Code must be indented with 4 spaces.

```js
// Good
function greet(name) {
    return `Hello ${name}!`;
}

// Bad, only 2 spaces.
function greet(name) {
  return `Hello ${name}!`;
}
```

When it comes to spaces around symbols or keywords, the rule of thumb is: add them. Everything in this section should be handled by ESLint.

```js
// Good
if (true) {
    // ...
} else {
    // ...
}

// Bad, needs more spaces.
if(true){
    // ...
}else{
    // ...
}
```

Infix operators need room to breath.

```js
// Good
const two = 1 + 1;

// Bad, needs more spaces.
const two = 1+1;
```

Braces should always be on the same as it's corresponding statement or declaration (known as *the one true brace style*).

```js
// Good
if (true) {
    // ...
}

// Bad
if (true)
{
    // ...
}
```

Named functions don't need a space before their parameters. Anonymous ones do.

```js
// Good
function save(user) {
    // ...
}

// Bad, no space before the parameters.
function save (user) {
    // ...
}
```

```js
// Good
save(user, function (response) {
    // ...
});

// Bad, anonymous functions require a space before the parameters.
save(user, function(response) {
    // ...
});
```

### Spacing and Indentation in Objects and Arrays

Objects and arrays require spaces between their braces and brackets. Arrays that contain an object or another array mustn't have a space between the brackets. Multiline objects and arrays require trailing commas.

```js
// Good
const person = { name: 'Sebastian', job: 'Developer' };

// Bad, no spaces between parentheses.
const person = {name: 'Sebastian', job: 'Developer'};
```

```js
// Good
const person = {
    name: 'Sebastian',
    job: 'Developer',
};

// Bad, no trailing comma.
const person = {
    name: 'Sebastian',
    job: 'Developer'
};
```

```js
// Good
const pairs = [['a', 'b'], ['c', 'd']];
const people = [{ name: 'Sebastian' }, { name: 'Willem' }];

// Bad, no extra spaces if the array contains arrays or objects.
const pairs = [ ['a', 'b'], ['c', 'd'] ];
const people = [ { name: 'Sebastian' }, { name: 'Willem' } ];
```

### Line Length

Lines shouldn't be longer than 100 characters, and mustn't be longer than 120 characters (the former isn't enforced by ESLint). Comments mustn't be longer than 80 characters.

### Quotes

Use single quotes if possible. If you need multiline strings or interpolation, use template strings.

```js
// Good
const company = 'Spatie';

// Bad, single quotes can be used here.
const company = "Spatie";

// Bad, single quotes can be used here.
const company = `Spatie`;
```

```js
// Good
function greet(name) {
    return `Hello ${name}!`;
}

// Bad, template strings are preferred.
function greet(name) {
    return 'Hello ' + name + '!';
}
```

Also, when writing html templates (or jsx for that matter), start multiline templates on a new line.

```js
function createLabel(text) {
    return `
        <div class="label">
            ${text}
        </div>
    `;
}
```

### Semicolons

Always.

### Variable Assignment

Prefer `const` over `let`. Only use `let` to indicate that a variable will be reassigned. Never use `var`.

### Variable Names

Variable names generally shouldn't be abbreviated.

```js
// Good
function saveUser(user) {
    localStorage.set('user', user);
}

// Bad, it's hard to reason about abbreviations in blocks as they grow.
function saveUser(u) {
    localStorage.set('user', u);
}
```

In single-line arrow functions, abbreviations are allowed to reduce noise if the context is clear enough. For example, if you're calling `map` of `forEach` on a collection of items, it's clear that the parameter is an item of a certain type, which can be derived from the collection's substantive variable name.

```js
// Good
function saveUserSessions(userSessions) {
    userSessions.forEach(s => saveUserSession(s));
}

// Ok, but pretty noisy.
function saveUserSessions(userSessions) {
    userSessions.forEach(userSession => saveUserSession(userSession));
}
```

### Comparisons

Always use a triple equal to do variable comparisons. If you're unsure of the type, cast it first.

```js
// Good
const one = 1;
const another = "1";

if (one === parseInt(another)) {
    // ...
}

// Bad
const one = 1;
const another = "1";

if (one == another) {
    // ...
}
```

### Function Keyword vs. Arrow Functions

Function declarations should use the function keyword.

```js
// Good
function scrollTo(offset) {
    // ...
}

// Using an arrow function doesn't provide any benefits here, while the
// `function`  keyword immediately makes it clear that this is a function.
const scrollTo = (offset) => {
    // ...
};
```

Terse, single line functions can also use the arrow syntax. There's no hard rule here.

```js
// Good
function sum(a, b) {
    return a + b;
}

// It's a short and simple method, so squashing it to a one-liner is ok.
const sum = (a, b) => a + b;
```

```js
// Good
export function query(selector) {
    return document.querySelector(selector);
}

// This one's a bit longer, having everything on one line feels a bit heavy.
// It's not easily scannable unlike the previous example.
export const query = selector => document.querySelector(selector);
```

Higher order functions can use arrow functions if it improves readability.

```js
function sum(a, b) {
    return a + b;
}

// Good
const adder = a => b => sum(a, b);

// Ok, but unnecessarily noisy.
function adder(a) {
    return b => sum(a, b);
}
```

Anonymous functions should use arrow functions.

```js
['a', 'b'].map(a => a.toUpperCase());
```

Unless they need access to `this`.

```js
$('a').on('click', function () {
    window.location = $(this).attr('href');
});
```

> Try to keep your functions pure and limit the usage of the `this` keyword!

Object methods must use the shorthand method syntax.

```js
// Good
export default {
    methods: {
        handleClick(event) {
            event.preventDefault();
        },
    },
};

// Bad, the `function` keyword serves no purpose.
export default {
    methods: {
        handleClick: function (event) {
            event.preventDefault();
        },
    },
};

// Bad, it's common for object methods to require context (`this`), so you'd
// end up with a mix of syntaxes.
export default {
    methods: {
        handleClick: e => e.preventDefault(),
        save() {
            this.user.save();
        },
    },
};
```

### Arrow Function Parameter Brackets

An arrow function's parameter brackets must be omitted if the function is a one-liner.

```js
// Good
['a', 'b'].map(a => a.toUpperCase());

// Bad, the parentheses are noisy.
['a', 'b'].map((a) => a.toUpperCase());
```

If the arrow function has it's own block, parameters must be surrounded by brackets.

```js
// Good, although according to this style guide you shouldn't be using an
// arrow function here!
const saveUser = (user) => {
    //
};

// Bad
const saveUser = user => {
    //
};
```

If you're writing a higher order function, you should emit the parentheses even if the returned function has braces.

```js
// Good
const adder = a => b => {
    sum(a, b);
};

// Bad, looks inconsistent in this context.
const adder = a => (b) => {
    sum(a, b);
};
```

### Object and Array Destructuring

Destructuring is preferred over assigning variables to the corresponding keys.

```js
// Good
const [ hours, minutes ] = '12:00'.split(':');

// Bad, unnecessarily verbose, and requires an extra assignment in this case.
const time = '12:00'.split(':');
const hours = time[0];
const minutes = time[1];
```

Destructuring is very valuable for passing around configuration-like objects.

```js
function uploader({
    element,
    url,
    multiple = false,
    beforeUpload = noop,
    afterUpload = noop,
}) {
    // ...
}
```

## Credits

This style guide is mainly inspired by the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript), and [Benjamin De Cock's frontend guidelines](https://github.com/bendc/frontend-guidelines).
