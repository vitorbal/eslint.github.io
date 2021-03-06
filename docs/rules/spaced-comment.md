---
title: Rule spaced-comment
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Requires or disallows a whitespace (space or tab) beginning a comment (spaced-comment)

(fixable) The `--fix` option on the [command line](../user-guide/command-line-interface#fix) automatically fixes problems reported by this rule.

Some style guides require or disallow a whitespace immediately after the initial `//` or `/*` of a comment.
Whitespace after the `//` or `/*` makes it easier to read text in comments.
On the other hand, commenting out code is easier without having to put a whitespace right after the `//` or `/*`.

## Rule Details

This rule will enforce consistency of spacing after the start of a comment `//` or `/*`. It also provides several
exceptions for various documentation styles.

## Options

The rule takes two options.

* The first is a string which be either `"always"` or `"never"`. The default is `"always"`.

    * If `"always"` then the `//` or `/*` must be followed by at least one whitespace.

    * If `"never"` then there should be no whitespace following.

* This rule can also take a 2nd option, an object with any of the following keys: `"exceptions"` and `"markers"`.

    * The `"exceptions"` value is an array of string patterns which are considered exceptions to the rule.
    Please note that exceptions are ignored if the first argument is `"never"`.

    ```json
    "spaced-comment": ["error", "always", { "exceptions": ["-", "+"] }]
    ```

    * The `"markers"` value is an array of string patterns which are considered markers for docblock-style comments,
    such as an additional `/`, used to denote documentation read by doxygen, vsdoc, etc. which must have additional characters.
    The `"markers"` array will apply regardless of the value of the first argument, e.g. `"always"` or `"never"`.

    ```json
    "spaced-comment": ["error", "always", { "markers": ["/"] }]
    ```

The difference between a marker and an exception is that a marker only appears at the beginning of the comment whereas
exceptions can occur anywhere in the comment string.

You can also define separate exceptions and markers for block and line comments. The `"block"` object can have an additional key `"balanced"`, a boolean that specifies if inline block comments should have balanced spacing. The default value is `false`.

* If `"balanced": true` and `"always"` then the `/*` must be followed by at least one whitespace, and the `*/` must be preceded by at least one whitespace.

* If `"balanced": true` and `"never"` then there should be no whitespace following `/*` or preceding `*/`.

* If `"balanced": false` then balanced whitespace is not enforced.

```json
"spaced-comment": ["error", "always", {
    "line": {
        "markers": ["/"],
        "exceptions": ["-", "+"]
    },
    "block": {
        "markers": ["!"],
        "exceptions": ["*"],
        "balanced": true
    }
}]
```

### always

The following patterns are considered problems:

```js
/*eslint spaced-comment: ["error", "always"]*/

//This is a comment with no whitespace at the beginning

/*This is a comment with no whitespace at the beginning */
```

```js
/* eslint spaced-comment: ["error", "always", { "block": { "balanced": true } }] */
/* This is a comment with whitespace at the beginning but not the end*/
```

The following patterns are not considered problems:

```js
/* eslint spaced-comment: ["error", "always"] */

// This is a comment with a whitespace at the beginning

/* This is a comment with a whitespace at the beginning */

/*
 * This is a comment with a whitespace at the beginning
 */

/*
This comment has a newline
*/
```

```js
/* eslint spaced-comment: ["error", "always"] */

/**
* I am jsdoc
*/
```

### never

The following patterns are considered problems:

```js
/*eslint spaced-comment: ["error", "never"]*/

// This is a comment with a whitespace at the beginning

/* This is a comment with a whitespace at the beginning */

/* \nThis is a comment with a whitespace at the beginning */
```

```js
/*eslint spaced-comment: ["error", "never", { "block": { "balanced": true } }]*/
/*This is a comment with whitespace at the end */
```

The following patterns are not considered problems:

```js
/*eslint spaced-comment: ["error", "never"]*/

/*This is a comment with no whitespace at the beginning */
```

```js
/*eslint spaced-comment: ["error", "never"]*/

/**
* I am jsdoc
*/
```

### exceptions

The following patterns are considered problems:

```js
/* eslint spaced-comment: ["error", "always", { "block": { "exceptions": ["-"] } }] */

//--------------
// Comment block
//--------------
```

```js
/* eslint spaced-comment: ["error", "always", { "exceptions": ["-", "+"] }] */

//------++++++++
// Comment block
//------++++++++
```

```js
/* eslint spaced-comment: ["error", "always", { "exceptions": ["-", "+"] }] */

/*------++++++++*/
/* Comment block */
/*------++++++++*/
```

```js
/* eslint spaced-comment: ["error", "always", { "line": { "exceptions": ["-+"] } }] */

/*-+-+-+-+-+-+-+*/
// Comment block
/*-+-+-+-+-+-+-+*/
```

The following patterns are not considered problems:

```js
/* eslint spaced-comment: ["error", "always", { "exceptions": ["-"] }] */

//--------------
// Comment block
//--------------
```

```js
/* eslint spaced-comment: ["error", "always", { "line": { "exceptions": ["-"] } }] */

//--------------
// Comment block
//--------------
```

```js
/* eslint spaced-comment: ["error", "always", { "exceptions": ["*"] }] */

/****************
 * Comment block
 ****************/
```

```js
/* eslint spaced-comment: ["error", "always", { "exceptions": ["-+"] }] */

//-+-+-+-+-+-+-+
// Comment block
//-+-+-+-+-+-+-+

/*-+-+-+-+-+-+-+*/
// Comment block
/*-+-+-+-+-+-+-+*/
```

```js
/* eslint spaced-comment: ["error", "always", { "block": { "exceptions": ["-+"] } }] */

/*-+-+-+-+-+-+-+*/
// Comment block
/*-+-+-+-+-+-+-+*/
```

### markers

The following patterns are considered problems:

```js
/* eslint spaced-comment: ["error", "always", { "markers": ["/"] }] */

///This is a comment with a marker but without whitespace
```

```js
/*eslint spaced-comment: ["error", "always", { "block": { "markers": ["!"], "balanced": true } }]*/
/*! This is a comment with a marker but without whitespace at the end*/
```

```js
/*eslint spaced-comment: ["error", "never", { "block": { "markers": ["!"], "balanced": true } }]*/
/*!This is a comment with a marker but with whitespace at the end */
```

The following patterns are not considered problems:

```js
/* eslint spaced-comment: ["error", "always", { "markers": ["/"] }] */

/// This is a comment with a marker
```

```js
/*eslint spaced-comment: ["error", "never", { "markers": ["!<"] }]*/

//!<This is a line comment with a marker

/*!<this is a block comment with a marker
subsequent lines are ignored
*/
```

```js
/* eslint spaced-comment: ["error", "always", { "markers": ["global"] }] */

/*global ABC*/
```


## Related Rules

* [spaced-line-comment](spaced-line-comment)

## Version

This rule was introduced in ESLint 0.23.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/spaced-comment.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/spaced-comment.md)
