# JavaScript Style Guide

A work in progress JavaScript style guide for our projects at [Spatie](https://spatie.be).

## Code Style

### Variable Assignment

Prefer `const` over `let`. Only use `let` to indicate that a variable will be reassigned. Never use `var`.

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
export const query = selector => document.querySelector(selector);
```

Higher order functions can use arrow functions if it improves readability.

```js
function sum(a, b) {
    return a + b;
}

// Good
const adder = a => b => sum(a, b);

// Ok, but pretty noisy.
function adder(a) {
    return function (b) {
        return sum(a, b);
    }
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
