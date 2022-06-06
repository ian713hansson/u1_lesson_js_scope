# JavaScript Scope

![Scope](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fblog.alexdevero.com%2Fwp-content%2Fuploads%2F2020%2F03%2F09-03-20-javascript-scope-explained-blog.jpg&f=1&nofb=1)

## Lesson Overview
In this lesson, we will discuss the concept of scope as it relates to programming in JavaScript.

## Objectives
- Learn what a block is.
- Discuss the difference between global and local scope in JavaScript.
- Identify which part(s) of JavaScript create new scope.
- Identify which variables are accessible in various scopes.

### Discussion

One best practice when coding is to only allow a piece of code to access the things it needs to access, and nothing more. To reduce interdependency and lower [coupling](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29), we can separate code into groups, called blocks.These blocks help enforce specific environmental context for our variables AKA scope.

Why might software developers want to keep certain objects and data separate from other parts of an application?

![Lego](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fmedia1.tenor.com%2Fimages%2F2b6aa507c3140c061fc980a29db8de56%2Ftenor.gif%3Fitemid%3D7976145&f=1&nofb=1)

### Blocks

A Block statement is used to group code together. To create a block, we use a pair of curly braces:
<!-- start code block file="snippets/block.js" -->
```js
{
  // The inside of a multiline block
}
```
<!-- end code block -->

Blocks are also used in functions, conditionals and loops:
<!-- start code block file="snippets/block-examples.js" -->
```js
if ( /* true || false */ ) { /* within the block, body of conditional */  }
for ( /* let i = 0; ...*/ ) { /* within the block, body of loop */ }
while ( /* i < num ... */ ) { /* within the block, body of loop */ }
function ( /* arg1, arg2 */ ) { /* within the block, body of function */ }
```
<!-- end code block -->

In addition to grouping code together, a block creates a new, _localized_, scope for the variables defined within the block.

### Scope
When declaring variables using the ES6 `let` and `const` initializers inside of a code block, these variables have _block scope_, meaning the variables are only recognized in the scope of the block they have been created (or declared) in.

You can think of scope as a collection of nested boxes. Each scope acts as a container in which variables and functions can be declared. While JavaScript is executing code within a scope, it only has access to variables declared in the current scope, parent scopes, and the global scope.

Scopes in JavaScript come in two flavors: *block scope* and *function scope*. When you create a function, that function has it's own scope.  Any variables defined within a function can only be accessed in the scope of that function.

**The following are examples of block and function scopes:**
<!-- start code block file="snippets/scope-creation.js" -->
```js
{ /* creates block scope */ }

if { /* creates block scope */ }
for ( /* ... */ ) { /* creates block scope */ }
while ( /* ... */ ) { /* creates block scope */ }
function ( /* ... */ ) { /* creates a function scope */ }
```
<!-- end code block -->

#### Demo - Identifying Global and Local (block) scopes

The outer most scope of a program is the _global scope_ and all block and function scopes are considered _local scopes_. Variables are accessible within the scope they are declared:

<!-- start code block file="snippets/block-scope.js" -->
```js
const name = 'Danny' // this variable is being declared in the "global scope"
{
  const name = 'Caleb'  // this variable is being declared in a "block scope"
}
console.log(name) // prints 'Danny' because this line is being run in the global scope and NOT the block scope of the program.

// name = 'Caleb' is limited in scope to the block in which it is defined
```
<!-- end code block -->

Variables are _also_ accessible to any inner scopes (child scopes) and can be reassigned locally without modifying the value on a global level.:

<!-- start code block file="snippets/child-scope-vars.js" -->
```js
// global scope
let x = 1

if (true) {
  // local scope
  x = 2
  console.log(x) // Since x modified in the local scope the output will be 2
}
// global scope
console.log(x)  // Since this line is outside of the local scope the output will be 1
```
<!-- end code block -->

However, variables declared in local scopes are not accessible to parent scopes:

<!-- start code block file="snippets/parent-scope-vars.js" -->
```js
// global scope
const x = 1

if (true) {
  // local scope
  const y = x // we declare a variable of y and assign it the value found in x
  console.log(y)  // 1
}
// global scope
console.log(x)  // 1
console.log(y)  // ReferenceError: y is not defined <-- we get this error because y is not declared in the global scope.
```
<!-- end code block -->

Variables are not accessible from sibling scopes:
<!-- start code block file="snippets/sibling-scope.js" -->
```js
if (true) {
  // local scope of 1st sibling
  const a = 1
  console.log(a) // 1
}

if (true) {
  // local scope of 2nd sibling
  console.log(a) // ReferenceError: a is not defined
}
```
<!-- end code block -->

Different scopes can have variables that are declared with the same name and
they do not conflict or know about each other.
<!-- start code block file="snippets/different-scope-vars.js" -->
```js
// global scope
const x = 1
console.log(x) // 1

if (true) {
  // local scope
  const x = 2
  console.log(x) // 2
}
// global scope
console.log(x) // 1
```
<!-- end code block -->

As we have seen, utilizing scope provides great utility. Scoping provides a way to __encapsulate__ data and prevent other parts of our applciation from accessing variables declared within a certain scope. By being aware of how scope is created, and by using scope effectively, you will write code that is more efficient, organized and less error prone.

![whew](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fmedia.giphy.com%2Fmedia%2FijGS9TME6iN7W%2Fgiphy.gif&f=1&nofb=1)

#### Best Practices:
- Apply the [Principle of Least Privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege): Allow code to access the information and resources that are necessary for it to run, and nothing more.
- Encapsulate code as much as possible in scope using functions and blocks


## Lesson Recap

In JavaScript, we use scope to encapsulate data and hide it from other parts of our application. The most common way to create a new scope is with a function. We can also create scope using a block. By using scope, we can keep our code organized, manageable, avoid variable name collision, and keep the global namespace clean.

![Cap](http://24.media.tumblr.com/95c072f1d694c3b132614ac3dc40fdcc/tumblr_ms6qvrVCJm1rdnvweo1_500.gif)

## Resources
- [Coupling](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29)
- [MDN - Break](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/break)
- [MDN - Blocks](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/block)
- [MDN - Scope](https://developer.mozilla.org/en-US/docs/Glossary/Scope)
