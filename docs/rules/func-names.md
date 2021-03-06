---
title: Rule func-names
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Require or disallow named `function` expressions (func-names)

A pattern that's becoming more common is to give function expressions names to aid in debugging. For example:

```js
Foo.prototype.bar = function bar() {};
```

Adding the second `bar` in the above example is optional.  If you leave off the function name then when the function throws an exception you are likely to get something similar to `anonymous function` in the stack trace.  If you provide the optional name for a function expression then you will get the name of the function expression in the stack trace.

## Rule Details

This rule can enforce or disallow the use of named function expressions.

## Options

This rule has a string option:

* `"always"` (default) requires function expressions to have a name
* `"never"` disallows named function expressions, except in recursive functions, where a name is needed


Examples of **incorrect** code for this rule with the default `"always"` option:

```js
/*eslint func-names: "error"*/

Foo.prototype.bar = function() {};

(function() {
    // ...
}())
```

Examples of **correct** code for this rule with the default `"always"` option:

```js
/*eslint func-names: "error"*/

Foo.prototype.bar = function bar() {};

(function bar() {
    // ...
}())
```

Examples of **incorrect** code for this rule with the `"never"` option:

```js
/*eslint func-names: "error"*/

Foo.prototype.bar = function bar() {};

(function bar() {
    // ...
}())
```

Examples of **correct** code for this rule with the `"never"` option:

```js
/*eslint func-names: "error"*/

Foo.prototype.bar = function() {};

(function() {
    // ...
}())
```

## Further Reading

* [Functions Explained](http://markdaggett.com/blog/2013/02/15/functions-explained/)

## Compatibility

* **JSCS**: [requireAnonymousFunctions](http://jscs.info/rule/requireAnonymousFunctions)
* **JSCS**: [disallowAnonymousFunctions](http://jscs.info/rule/disallowAnonymousFunctions)

## Version

This rule was introduced in ESLint 0.4.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/func-names.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/func-names.md)
