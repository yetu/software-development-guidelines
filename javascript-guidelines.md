# Main goals

* Be consistent, but not religious about the style.
* Use tools to keep aligned with the guidelines.
* Strive for readable code and simple expressions.
* Eliminate all inconsistencies you spot.
* Strive for Functional Programming style.

## Whitespaces

* Space indentation for all files (2 spaces). See [.editorconfig](.editorconfig)
* Smart tabs are ok.
* Use one space after `if`, `for`, `while`, etc.
* Use one space after `function` for anonymous functions but not for named functions:
```javascript
var fn = function () {}
function fn() {}
```
* Don't leave trailing whitespace at the end of lines.

## Variables
* Use one `var` per variable unless you don't assign any values to it (and it's short enough):
```javascript
var smth = 123
var next, prev, idx
```
* Use lowerCamelCase for variables and properties.
* User UPPERCASE for constants.

## Comments
* Comment all non-obvious stuff.

## Functions
* Use named functions. They make stack traces a lot easier to read.
* Avoid anonymous functions in chains.
* Use lowerCamelCase for function and method names.
* User UpperCamelCase for class names.

## General style requirements
* [1TBS](http://en.wikipedia.org/wiki/Indent_style#Variant:_1TBS)
* **Single quotes** for strings, unless you are writing JSON.
* **Leading dot** for chain calls.
* `use strict;`
* Use `===` operator.
* Write small functions (no more than 15 expressions).
* Avoid deeply nested expressions (max depth = 3).
* All projects **must** have pre-commit hooks for linting (use [husky](https://github.com/typicode/husky)).
* Use [.jshintrc](.jshintrc) and [.editorconfig](.editorconfig)

## In case of emergency
Use [FixMyJS](https://github.com/jshint/fixmyjs)

## Inspired by

* [npm coding style](https://www.npmjs.org/doc/misc/npm-coding-style.html)
* [node style guide](https://github.com/felixge/node-style-guide)
