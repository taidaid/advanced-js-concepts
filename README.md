<!-- Copy and paste the converted output. -->

<!-----
NEW: Check the "Suppress top comment" option to remove this info from the output.

Conversion time: 8.076 seconds.


Using this Markdown file:

1. Paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β29
* Sat Jan 30 2021 00:51:43 GMT-0800 (PST)
* Source doc: Advanced JavaScript Concepts

WARNING:
H6 not demoted to H7. Look for "H6 not demoted to H7." inline.

* Tables are currently converted to HTML tables.
* This document has images: check for >>>>>  gd2md-html alert:  inline image link in generated source and store images to your server. NOTE: Images in exported zip file from Google Docs may not appear in  the same order as they do in your doc. Please check the images!

----->

<p style="color: red; font-weight: bold">>>>>>  gd2md-html alert:  ERRORs: 0; WARNINGs: 1; ALERTS: 35.</p>
<ul style="color: red; font-weight: bold"><li>See top comment block for details on ERRORs and WARNINGs. <li>In the converted Markdown or HTML, search for inline alerts that start with >>>>>  gd2md-html alert:  for specific instances that need correction.</ul>

<a href="#gdcalert7">alert7</a>
<a href="#gdcalert8">alert8</a>
<a href="#gdcalert9">alert9</a>
<a href="#gdcalert10">alert10</a>
<a href="#gdcalert11">alert11</a>
<a href="#gdcalert12">alert12</a>
<a href="#gdcalert13">alert13</a>
<a href="#gdcalert14">alert14</a>
<a href="#gdcalert15">alert15</a>
<a href="#gdcalert16">alert16</a>
<a href="#gdcalert17">alert17</a>
<a href="#gdcalert18">alert18</a>
<a href="#gdcalert19">alert19</a>
<a href="#gdcalert20">alert20</a>
<a href="#gdcalert21">alert21</a>
<a href="#gdcalert22">alert22</a>
<a href="#gdcalert23">alert23</a>
<a href="#gdcalert24">alert24</a>
<a href="#gdcalert25">alert25</a>
<a href="#gdcalert26">alert26</a>
<a href="#gdcalert27">alert27</a>
<a href="#gdcalert28">alert28</a>
<a href="#gdcalert29">alert29</a>
<a href="#gdcalert30">alert30</a>
<a href="#gdcalert31">alert31</a>
<a href="#gdcalert32">alert32</a>
<a href="#gdcalert33">alert33</a>
<a href="#gdcalert34">alert34</a>
<a href="#gdcalert35">alert35</a>

<p style="color: red; font-weight: bold">>>>>> PLEASE check and correct alert issues and delete this message and the inline alerts.<hr></p>

# Advanced JavaScript Concepts

### A reference guide for Advanced JavaScript Concepts

This guide is <span style="text-decoration:underline;">incomplete</span>! Please **contact me** to add knowledge and ask questions. Sorry, but comments have been disabled, a few too many accidental edits/comments.

[A Map for the Advanced JavaScript Concepts Course](https://coggle.it/diagram/XE3ZoVj-rtA5hcxj/t/advanced-javascript)

[Acknowledgements](#bookmark=id.1irietpnj5)

## JavaScript Foundation

### Section 1

#### JavaScript Engine

- An **engine **is responsible for providing the mechanics of parsing and JIT compilation, i.e. producing machine-executable operations from a script written in JavaScript.
- Translates JS into something a computer can understand
- Many Engines:
  - All JS Engines should comply with ECMAScript standards
  - Examples:
    - V8 (Chrome)
    - Chakra (MS Edge)
    - Nitro (Safari)
    - SpiderMonkey (Firefox)
- JS Creator and first JS Engine author
  - Brendan Eich

_How the JS engine works_

![javascript engine](https://i.imgur.com/AOq7MU5.png)

- Parser
  - Lexical Analysis
    - Code is parsed into “tokens”
- AST
  - Tokens form an “Abstract Syntax Tree” (AST)
  - [Practical AST Examples](Astexplorer.net)
- Bytecode
  - Not as low-level as machine code, but a lower level than JS
- Profiler/Monitor
  - Watches code and optimizes
  - If it sees an opportunity to optimize, e.g. a loop with same input/output, it passes the code to the JIT compiler
- Compiler
  - Creates optimized machine code
- Single-threaded
  - The call stack only executes one function at a time
  - We circumvent the limitations of ‘single-threadedness’ with the Web API
- Hidden Classes - A Common "Gotcha"

  - When instantiating new objects, the compiler will try to create a common ‘hidden class’. By defining properties in different orders, the compiler will de-optimize the code.

  - When compiling, the compiler tries to optimize the code, for example, by creating "**hidden classes**": [V8 Hidden class](https://engineering.linecorp.com/en/blog/v8-hidden-class/)
    - There are cases where the code can be optimized by the compiler by _sharing_ "**hidden classes**", but for some reason, such as a _different order of object property creation_, the compiler mistakenly thinks that two objects, which should be able to share "**hidden classes**", cannot. The compiler is thus creating an unnecessary inefficiency which we call "_de-optimizing the code_".

  * Also see:
    - [https://marcradziwill.com/blog/mastering-javascript-high-performance/#hiddenclasses](https://marcradziwill.com/blog/mastering-javascript-high-performance/#hiddenclasses)
    - [The case of temporary objects in Chrome](https://benediktmeurer.de/2016/10/11/the-case-of-temporary-objects-in-chrome/)
    - [Optimizing compiler](#bookmark=id.z8rggew72vka)
  * This means that we should either set all possible properties in the constructor of a class
  * Or we can be careful to always define new properties in the same order

```
  function Animal(x, y) {
    this.x = x;
    this.y = y;
  }
  const obj1 = new Animal(1,2)
  const obj2 = new Animal(3,4)
  // Here the objects are given new properties, but in different orders
  obj1.a = 1
  obj1.b = 2
  obj2.b = 2
  obj2.a = 1
```

---

#### JavaScript Runtime

- The **runtime** environment _provides the built-in libraries that are available to the program at runtime_ (during execution). So, if you're going to use the Window object or the DOM API in the browser, those would be included in the browser's JS runtime environment. A Node.js runtime includes different libraries, say, the Cluster and FileSystem APIs. Both runtimes include the built-in data types and common facilities such as the Console object.

#### JavaScript Engine vs. Runtime

- The distinction between the two is not always clear and you'll find that the terms are commonly used interchangeably.
- Chrome and Node.js share the _same **engine **_(Google's V8), but they have _different **runtime **_(execution) environments.
- In a way, the **runtime **is to the **engine **what the linker is to the compiler in a traditional compiled language.

[[https://www.quora.com/What-is-the-difference-between-javascript-engine-and-javascript-runtime](https://www.quora.com/What-is-the-difference-between-javascript-engine-and-javascript-runtime)]

---

#### <p style="text-align: right">

Interpreter/Compiler/JIT Compiler</p>

_Shows how JavaScript is translated into a lower-level language_

![JS Engine Compiles to Machine Language](https://i.imgur.com/bwv6BvU.png "JS Engine Compiles to Machine Language")

##### Interpreter vs Compiler

- Interpreter
  - Line by line
  - Faster to start
- Compiler
  - Reads entire file and translates to a lower level language
  - Once begun, is faster than interpreted by optimizing into a lower level language
  - Not perfect, can accidentally de-optimize code

---

##### JIT Compiler

###### “Just-In-Time” Compiler

As a way of getting rid of the interpreter’s inefficiency—where the interpreter has to keep retranslating the code every time they go through the loop—browsers started mixing compilers in.

Different browsers do this in slightly different ways, but the basic idea is the same. They added a new part to the JavaScript engine, called a monitor (aka a profiler). That monitor watches the code as it runs, and makes a note of how many times it is run and what types are used.

At first, the monitor just runs everything through the interpreter.

If the same lines of code are run a few times, that segment of code is called warm. If it’s run a lot, then it’s called hot.

---

###### Baseline compiler

When a function starts getting warm, the JIT will send it off to be compiled. Then it will store that compilation.

Each line of the function is compiled to a “stub”. The stubs are indexed by line number and variable type (I’ll explain why that’s important later). If the monitor sees that execution is hitting the same code again with the same variable types, it will just pull out its compiled version.

That helps speed things up. But like I said, there’s more a compiler can do. It can take some time to figure out the most efficient way to do things… to make optimizations.

The baseline compiler will make some of these optimizations (I give an example of one below).

It doesn’t want to take too much time, though, because it doesn’t want to hold up execution too long.

However, if the code is really hot—if it’s being run a whole bunch of times—then it’s worth taking the extra time to make more optimizations.

---

###### Optimizing compiler

When a part of the code is very hot, the monitor will send it off to the optimizing compiler. This will create another, even faster, version of the function that will also be stored.

In order to make a faster version of the code, the optimizing compiler has to make some assumptions.

For example, if it can assume that all objects created by a particular constructor have the same shape—that is, that they always have the same property names, and that those properties were added in the same order— then it can cut some corners based on that.

The optimizing compiler uses the information the monitor has gathered by watching code execution to make these judgments. If something has been true for all previous passes through a loop, it assumes it will continue to be true.

But of course with JavaScript, there are never any guarantees. You could have 99 objects that all have the same shape, but then the 100th might be missing a property.

So the compiled code needs to check before it runs to see whether the assumptions are valid. If they are, then the compiled code runs. But if not, the JIT assumes that it made the wrong assumptions and trashes the optimized code.

Then execution goes back to the interpreter or baseline compiled version. This process is called deoptimization (or bailing out).

Usually optimizing compilers make code faster, but sometimes they can cause unexpected performance problems. If you have code that keeps getting optimized and then deoptimized, it ends up being slower than just executing the baseline compiled version.

Most browsers have added limits to break out of these optimization/deoptimization cycles when they happen. If the JIT has made more than, say, 10 attempts at optimizing and keeps having to throw it out, it will just stop trying.

###### An example optimization: Type specialization

There are a lot of different kinds of optimizations, but I want to take a look at one type so you can get a feel for how optimization happens. One of the biggest wins in optimizing compilers comes from something called type specialization.

The dynamic type system that JavaScript uses requires a little bit of extra work at runtime. For example, consider this code:

```
function arraySum(arr) {
  var sum = 0;
  for (var i = 0; i < arr.length; i++) {
    sum += arr[i];
  }
}
```

The `+=` step in the loop may seem simple. It may seem like you can compute this in one step, but because of dynamic typing, it takes more steps than you would expect.

Let’s assume that `arr` is an array of 100 integers. Once the code warms up, the baseline compiler will create a stub for each operation in the function. So there will be a stub for `sum += arr[i]`, which will handle the `+=` operation as integer addition.

However,`sum` and `arr[i]` aren’t guaranteed to be integers. Because types are dynamic in JavaScript, there’s a chance that in a later iteration of the loop, `arr[i]` will be a string. Integer addition and string concatenation are two very different operations, so they would compile to very different machine code.

The way the JIT handles this is by compiling multiple baseline stubs. If a piece of code is monomorphic (that is, always called with the same types) it will get one stub. If it is polymorphic (called with different types from one pass through the code to another), then it will get a stub for each combination of types that has come through that operation.

This means that the JIT has to ask a lot of questions before it chooses a stub.

![JS JIT compiler Decision Tree](https://i.imgur.com/pW3JiZg.png "JS JIT compiler Decision Tree")

Because each line of code has its own set of stubs in the baseline compiler, the JIT needs to keep checking the types each time the line of code is executed. So for each iteration through the loop, it will have to ask the same questions.

The code would execute a lot faster if the JIT didn’t need to repeat those checks. And that’s one of the things the optimizing compiler does.

In the optimizing compiler, the whole function is compiled together. The type checks are moved so that they happen before the loop.

Some JITs optimize this even further. For example, in Firefox there’s a special classification for arrays that only contain integers. If `arr` is one of these arrays, then the JIT doesn’t need to check if `arr[i]` is an integer. This means that the JIT can do all of the type checks before it enters the loop.

###### Conclusion

That is the JIT in a nutshell. It makes JavaScript run faster by monitoring the code as it’s running it and sending hot code paths to be optimized. This has resulted in many-fold performance improvements for most JavaScript applications.

Even with these improvements, though, the performance of JavaScript can be unpredictable. And to make things faster, the JIT has added some overhead during runtime, including:

- optimization and deoptimization
- memory used for the monitor’s bookkeeping and recovery information for when bailouts happen
- memory used to store baseline and optimized versions of a function

There’s room for improvement here: that overhead could be removed, making performance more predictable. And that’s one of the things that WebAssembly does.

In the [next article](https://hacks.mozilla.org/?p=30503), I’ll explain more about assembly and how compilers work with it.

[by [Lin Clark](https://twitter.com/linclark) at [A crash course in just-in-time (JIT) compilers](https://hacks.mozilla.org/2017/02/a-crash-course-in-just-in-time-jit-compilers/)]

---

#### Writing Optimized Code

- Initialize objects of the same class in the same order

---

#### Call Stack + Memory Heap

- Call Stack
  - The call stack stores function calls
  - Ensures the program runs in order
  - The first stack frame (on top) is program’s current ‘location’
  - First In, Last Out
  - **Global Execution Context** is called and is at bottom of **Call Stack**
  - First function is called and is added to top of **Call Stack**
  - First function ‘returns’ and it is popped off of the **Call Stack**
  - Repeat until program completes and Global Execution Context pops off the Call Stack \* Stack Overflow is when there are too many stack frames, e.g.
  - Memory Heap
    - Stores values and references

```
function inception() {
  inception()
}
```

```
const number = 6; //allocate memory for number
const string = 'hello'; //allocate memory for a string
const human = { //allocate memory for an object and its values
  first: 'Bryan',
  last: 'James'
}
```

#####

---

#### Garbage Collection

- Garbage collection refers to a process that automatically frees up memory as it is able
- Garbage collection helps us avoid memory leaks
- Memory leaks are a failure in a program to release discarded memory, causing impaired performance or failure.
  - Global variables
  - Event listeners
    - For the case of observers, it is important to make explicit calls to remove them once they are not needed anymore (or the associated object is about to be made unreachable). In the past, this used to be particularly important as certain browsers (Internet Explorer 6) were not able to manage cyclic references well (see below for more info on that). Nowadays, most browsers can and will collect observer handlers once the observed object becomes unreachable, even if the listener is not explicitly removed. It remains good practice, however, to explicitly remove these observers before the object is disposed ([https://auth0.com/blog/four-types-of-leaks-in-your-javascript-code-and-how-to-get-rid-of-them/](https://auth0.com/blog/four-types-of-leaks-in-your-javascript-code-and-how-to-get-rid-of-them/))

```
var element = document.getElementById('button');

function onClick(event) {
 element.innerHtml = 'text';
}

element.addEventListener('click', onClick);
// Do stuff
element.removeEventListener('click', onClick);
element.parentNode.removeChild(element);
// Now when element goes out of scope,
// both element and onClick will be collected even in old browsers that don't handle cycles well.

```

- Mark and Sweep
  - JS can mark what references and values in memory are still needed
  - After marking, JS then **sweeps** out the unneeded memory

---

#### Node.js

- Node.js is a JS runtime
- It is written in C++

![Node.js Runtime](https://i.imgur.com/1tkBNVF.png)

![Node.js vs. PHP](https://i.imgur.com/nrBQ5gy.png "Node.js single main thread vs PHP multi-threaded I/O blocking execution")

####

---

#### Single Threaded Model

- JS is single-threaded
  - The call stack only executes one function at a time
- We circumvent the limitations of ‘single-threadedness’ with the Web API

###

---

### Section 2

#### Execution Context

- The environment in which the current code is being evaluated in. There can only be one execution context running at any point of time! This is because Javascript is single-threaded.
- **arguments** is an object that is made available to **execution contexts** made with the **function** keyword
  - Because **arguments** is an object, **Array** methods are not available
    - We can use **Array.from(arguments)** to create an array with the **arguments** values
  - The **spread** operator can be used to convert **arguments** in a **function** into an **Array**

####

---

#### Lexical Environment

- Lexical environments means where the code was written.
- The Global Environment is the parent environment to all other environments created in the code
- In the browser, the global environment is called **window**
- In Node.js, the global environment is called **global**

####

---

#### Hoisting

**Hoisting** is a term you will _not_ find used in any normative specification prose prior to [ECMAScript® 2015 Language Specification](http://www.ecma-international.org/ecma-262/6.0/index.html). **Hoisting** was thought up as a general way of thinking about how execution contexts (specifically the creation and execution phases) work in JavaScript. However, the concept can be a little confusing at first.

Conceptually, for example, a strict definition of **hoisting** suggests that **variable **and **function declarations **are physically moved to the top of your code, but this is not in fact what happens. Instead, the variable and function declarations are put into memory during the _compile_ phase, but stay exactly where you typed them in your code.

One of the advantages of JavaScript putting **function declarations **into memory before it executes any code segment is that _it allows you to use a **function **before you declare it in your code_. For example:

<table>
  <tr>
   <td><code>function catName(name) { </code>
<p>
<code>  console.log("My cat's name is " + name); </code>
<p>
<code>} </code>
<p>
<code>catName("Tigger"); /* The result of the code above is: "My cat's name is Tigger" */</code>
   </td>
  </tr>
  <tr>
   <td>
   </td>
  </tr>
</table>

The above code snippet is how you would expect to write the code for it to work. Now, let's see what happens when we call the **function **before we write it:

```
catName("Chloe");
function catName(name) {
  console.log("My cat's name is " + name);
} /* The result of the code above is: "My cat's name is Chloe" */
```

Even though we call the **function **in our code first, _before the **function **is written_, the code still works. This is because of how context execution works in JavaScript.

**Hoisting** works well with other data types and variables. The variables can be initialized and used before they are declared.

_JavaScript only **hoists** declarations, not initializations_. If a variable is declared and initialized after using it, the value will be undefined. For example:

```
console.log(num); // Returns undefined var num; num = 6;
```

If you declare the variable after it is used, but initialize it beforehand, it will return the value:

```
num = 6; console.log(num); // returns 6 var num;
```

Below are more examples demonstrating hoisting.

```
//Example 1 - Does not hoist
var x = 1; // Initialize x
console.log(x + " " + y); // '1 undefined'
var y = 2; // Initialize y
//This will not work as JavaScript only hoists declarations
//Example 2 - Hoists
var num1 = 3; //Declare and initialize num1
num2 = 4; //Initialize num2
console.log(num1 + " " + num2); //'3 4'
var num2; //Declare num2 for hoisting
//Example 3 - Hoists
a = 'Cran'; //Initialize a
b = 'berry'; //Initialize b
console.log(a + "" + b); // 'Cranberry'
var a, b; //Declare both a & b for hoisting
```

[[Hoisting - MDN Web Docs Glossary: Definitions of Web-related terms](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)]

##### Hoisting with const, let, and var

- **var** is the traditional way of declaring variables in JavaScript.
- ES6 (ECMAScript 6) introduced two new ways to declare variables, **const **and **let**, and are generally recommended in order to avoid unexpected hoisting complications.

###### var

- **var **has [function scope](#bookmark=id.2rhesqosl7ey)
- **var **declarations are **hoisted**, but _not the initialization_

      ```

  console.log(a); // undefined
  var a = 3;

````

- The above code is equivalent to the below code due to **hoisting**.

      ```

  var a;
  console.log(a); // undefined
  a=3;

````

###### const/let

- **const **and **let **have [block scope](#bookmark=id.eqpeekwmgxql)
- **const **and **let **declarations are _not **hoisted**_, so variables declared with **const/let** can only be accessed after their declaration in the code.

      ```

  console.log(a); //Uncaught ReferenceError: Cannot access 'a' before //initialization
  let a = 3;

console.log(b) //Uncaught ReferenceError: Cannot access 'b' before //initialization
const b = 3;

```





---



#### Function Invocation



*   The code inside a function_ is not executed_ when the function is **defined**.
*   The code inside a function_ is executed_ when the function is **invoked**.
*   It is common to use the term "call a function" instead of "invoke a function".
*   It is also common to say "call upon a function", "start a function", or "execute a function".


##### Invoking a Function as a Function


```

function myFunction(a, b) {
return a \* b;
}
myFunction(10, 2); // Will return 20

````

- The function above does not belong to any object. But in JavaScript there is always a default global object.
- In HTML the default global object is the HTML page itself, so the function above "belongs" to the HTML page.
- In a browser the page object is the browser window. The function above automatically becomes a window function.
- myFunction() and window.myFunction() is the same function:

      ```

  function myFunction(a, b) {
  return a \* b;
  }
  window.myFunction(10, 2); // Will also return 20

````

##### Invoking a Function as a Method

- In JavaScript you can define functions as object methods.
- The following example creates an object (myObject), with two properties (firstName and lastName), and a method (fullName):

      ```

  var myObject = {
  firstName:"John",
  lastName: "Doe",
  fullName: function () {
  return this.firstName + " " + this.lastName;
  }
  }
  myObject.fullName(); // Will return "John Doe"

````

- The fullName method is a function. The function belongs to the object. myObject is the owner of the function.
- The thing called this, is the object that "owns" the JavaScript code. In this case the value of this is myObject.

##### Invoking a Function with a Function Constructor

- If a **function invocation **is preceded with the _new_ keyword, it is a _constructor_ invocation.
- It looks like you create a new function, but since JavaScript functions are objects you actually create a new object:

      ```

  // This is a function constructor:
  function myFunction(arg1, arg2) {
  this.firstName = arg1;
  this.lastName = arg2;
  }

// This creates a new object
var x = new myFunction("John", "Doe");
x.firstName; // Will return "John"

````

- A constructor invocation creates a new object. The new object inherits the properties and methods from its constructor.
- The _this_ keyword in the constructor does not have a value.
- The value of _this_ will be the new object created when the function is invoked.

[[JavaScript Function Invocation](https://www.w3schools.com/js/js_function_invocation.asp)]

####

---

#### Scope

Scope determines the visibility or accessibility of a variable or other resource in the area of your code.

[[JavaScript: Introduction to Scope (function scope, block scope)](https://dev.to/sandy8111112004/javascript-introduction-to-scope-function-scope-block-scope-d11)]

##### Global Scope

There's only one **Global scope** in the JavaScript document. The area outside all the functions is considered the global scope and the variables defined inside the global scope can be accessed and altered in any other scopes.

```
//global scope
var fruit = 'apple'
console.log(fruit);        //apple

function getFruit(){
    console.log(fruit);    //fruit is accessible here
}

getFruit();                //apple
```

##### Local Scope

Variables declared inside the functions become **local** to the function and are considered in the corresponding **local scope**. _Every function has its own scope_. The same variable can be used in different functions because they are bound to the respective functions and are not mutually visible.

```
//global scope
function foo1(){
    //local scope 1
    function foo2(){
        //local scope 2
    }
}

//global scope
function foo3(){
    //local scope 3
}

//global scope
```

**Local scope** can be divided into **function scope** and **block scope**. The concept of **block scope** is introduced in ECMAscript 6 (ES6) together with the new ways to declare variables -- const and let.

##### Function Scope

Whenever you declare a variable in a function, the variable is visible only within the function. You can't access it outside the function. **var** is the keyword to define a variable for a function-scope accessibility.

```
function foo(){
    var fruit ='apple';
    console.log('inside function: ',fruit);
}

foo();                    //inside function: apple
console.log(fruit);       //error: fruit is not defined
```

##### Block Scope

A **block scope** is the area within if and switch conditions or for and while loops. Generally speaking, _whenever you see {curly brackets}_, it is a **block**. In ES6, **const** and **let** keywords allow developers to declare variables in the** block scope**, which means _those variables exist only within the corresponding block._

```
function foo(){
    if(true){
        var fruit1 = 'apple';        //exist in function scope
        const fruit2 = 'banana';     //exist in block scope
        let fruit3 = 'strawberry';   //exist in block scope

    }
    console.log(fruit1);
    console.log(fruit2);
    console.log(fruit3);
}

foo();
//result:
//apple
//error: fruit2 is not defined
//error: fruit3 is not defined
```

##### Lexical Scope

Another point to mention is the **lexical scope**. **Lexical scope** means the child scopes have access to the variables defined in the parent scope. _The child functions are lexically bound to the execution context of their parents._

##### Dynamic Scope

**Lexical scope** is the set of rules about how the _Engine_ can look-up a variable and where it will find it. The key characteristic of lexical scope is that it is defined at author-time, when the code is written (assuming you don't cheat with `eval()` or `with`).

Dynamic scope seems to imply, and for good reason, that there's a model whereby scope can be determined dynamically at runtime, rather than statically at author-time. That is in fact the case. Let's illustrate via code:

```
function foo() {
	console.log( a ); // 2
}

function bar() {
	var a = 3;
	foo();
}

var a = 2;

bar();
```

Lexical scope holds that the RHS reference to `a` in `foo()` will be resolved to the global variable `a`, which will result in value `2` being output.

**Dynamic scope**, by contrast, doesn't concern itself with how and where functions and scopes are declared, but rather where they are called from. In other words, the scope chain is based on the call-stack, not the nesting of scopes in code.

So, if JavaScript had dynamic scope, when `foo()` is executed, theoretically the code below would instead result in `3`as the output.

```
function foo() {
	console.log( a ); // 3  (not 2!)
}

function bar() {
	var a = 3;
	foo();
}

var a = 2;

bar();
```

How can this be? Because when `foo()` cannot resolve the variable reference for a, instead of stepping up the nested (lexical) scope chain, it walks up the call-stack, to find where `foo()` was _called from_. Since `foo()` was called from `bar()`, it checks the variables in scope for `bar()`, and finds an **_a_** there with value 3.

Strange? You're probably thinking so, at the moment.

But that's just because you've probably only ever worked on (or at least deeply considered) code which is lexically scoped. So dynamic scoping seems foreign. If you had only ever written code in a dynamically scoped language, it would seem natural, and lexical scope would be the odd-ball.

To be clear, **_JavaScript does not, in fact, have dynamic scope_**. It has **lexical scope**. Plain and simple. But the `this` mechanism is kind of like **dynamic scope**.

The key contrast: **lexical scope** is write-time, whereas **dynamic scope** (and `this`!) are runtime. **Lexical scope** cares _where a function was declared_, but **dynamic scope** cares where a function was _called from_.

Finally: `this` cares _how a function was called_, which shows how closely related the `this` mechanism is to the idea of **dynamic scoping**.

[[https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20%26%20closures/apA.md](https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20%26%20closures/apA.md)]

---

#### Context vs. Scope

- **Context **refers to the \_this \_keyword, i.e. the object
- **Scope** refers to the _visibility of variables_

---

#### Scope Chain

To understand the **scope chain** you must know how **[closures](#bookmark=id.bfvcuvp9bg6) **work.

A **closure **is formed when you nest functions, inner functions can refer to the variables present in their outer enclosing functions even after their parent functions have already executed.

JavaScript resolves identifiers within a particular context by traversing up the **scope chain**, moving from locally to globally.

Consider this example with three nested functions:

```
var currentScope = 0; // global scope
(function () {
  var currentScope = 1, one = 'scope1';
  alert(currentScope);
  (function () {
    var currentScope = 2, two = 'scope2';
    alert(currentScope);
    (function () {
      var currentScope = 3, three = 'scope3';
      alert(currentScope);
      alert(one + two + three); // climb up the scope chain to get one and two
    }());
  }());
}());
```

[[Scope Chain in Javascript](https://stackoverflow.com/questions/1484143/scope-chain-in-javascript)]

####

---

#### this - call, apply, bind

##### this

```
this
```

- “**this**” is the object which the function is a property of
- “**this**” gives functions access to their object and its properties
- “**this**” helps us execute the same code for multiple objects
- “**this**” can be thought of as “who called me?” i.e., what is to the left of the dot, such as window.a()
- “**this**” is **dynamically scoped**, i.e. it doesn’t matter where it was written, it matters where it was called

<p id="gdcalert9" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image9.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert10">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image9.png "image_tooltip")

<p id="gdcalert10" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image10.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert11">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image10.png "image_tooltip")

- **Arrow functions** bind “this” to the lexical scope

<p id="gdcalert11" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image11.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert12">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image11.png "image_tooltip")

##### call()

- function a() === function.call()
- **call()** takes* (&lt;object>, ...&lt;params>)*
- Calls a method of an object, substituting an object for the current object

<p id="gdcalert12" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image12.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert13">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image12.png "image_tooltip")

##### apply()

- **apply()** is the same as** call()** except that **call()** takes* (&lt;object>, ...&lt;params>)* and **apply()** takes _(&lt;object>, &lt;[array of params]>)_

##### bind()

- The** bind()** method creates a new function that, when called, has its **_this _**keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.
- _function_.**bind**(_thisArg_[, _arg1_[, _arg2_[, ...]]])
  _ *thisArg*
  _ The value to be passed as the **this **parameter to the target function when the bound function is called. The value is ignored if the bound function is constructed using the **new **operator. When using **bind **to create a function(supplied as a callback) inside a setTimeout, any **primitive **value passed as _thisArg \_is converted to **object**. If no arguments are provided to bind, the **this **of the executing scope is treated as the \_thisArg \_for the new function. \* \_arg1_, _arg2_, … \* Arguments to prepend to arguments provided to the bound function when invoking the target function.

              ```

  Function.prototype.bind = function(whoIsCallingMe){
  const self = this;
  return function(){
  return self.apply(whoIsCallingMe, arguments);
  };
  }

````

- **bind()** is especially useful for remedying the **dynamic scope** property of **_this_** by binding it to a lexical scope

      ```

  var module = {
  x: 42,
  getX: function() {
  return this.x;
  }
  }
  var unboundGetX = module.getX;
  console.log(unboundGetX()); // The function gets invoked at the global scope
  // expected output: undefined

var boundGetX = unboundGetX.bind(module);
console.log(boundGetX());
// expected output: 42

````

<p id="gdcalert13" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image13.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert14">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image13.png "image_tooltip")

---

#### Functions Expressions vs Function Statements

- An **expression **produces a value and can be written wherever a value is expected, for example as an argument in a function call
- Each line below is an expression

      ```

  myvar
  3 + x
  myfunc("a", "b")

````

- Roughly, a **statement **performs an action. **Loops **and **if statements** are examples of statements. A program is basically a sequence of statements (we’re ignoring declarations here). Wherever JavaScript expects a statement, you can also write an expression. Such a statement is called an _expression statement_. The reverse does not hold: you cannot write a statement where JavaScript expects an expression. For example, an if statement cannot become the argument of a function.
- **Expression**: produces a value
- **Statement**: performs an action
- **Expression statement**: produces a value and performs an action
- The following is an example of an **\_if \_statement**:

      ```

  var x;
  if (y >= 0) {
  x = y;
  } else {
  x = -y;
  }

````

- Expressions have an analog, the conditional operator. The above statements are equivalent to the following statement.

      ```

  var x = (y >= 0 ? y : -y);

```





---



#### IIFE


```

(function () {})() === (function (){}())
// undefined === undefined

````

- **Immediately Invoked Function Expressions** have been used in the past, before modules, to avoid polluting the namespace. It does this by limiting the scope of variables in the function to the function scope

      ```

  var script1 = (function () {
  function a() {
  return 5;
  }
  return {
  a: a
  }
  })()

````

#### Use Strict

- Strict mode makes it easier to write "secure" JavaScript.
- Strict mode changes previously accepted "bad syntax" into real errors.
- As an example, in normal JavaScript, mistyping a variable name creates a new global variable. In strict mode, this will throw an error, making it impossible to accidentally create a global variable.
- In normal JavaScript, a developer will not receive any error feedback assigning values to non-writable properties.
- In strict mode, any assignment to a non-writable property, a getter-only property, a non-existing property, a non-existing variable, or a non-existing object, will throw an error.
- [W3Schools](https://www.w3schools.com/js/js_strict.asp) has a good list of what is not allowed in strict mode

[[JavaScript "use strict"](https://www.w3schools.com/js/js_strict.asp)]

---

## Types In JavaScript

### Section 1

#### Static vs. Dynamically Typed

- JS is both **dynamically typed** and **weakly typed**.
- **Statically typed** means the type is enforced and won’t change so easily. All variables must be declared with a type.
- **Static Typing** is exemplified by C++ and Java’s use of variable declaration

      ```

  int a == 100 // explicitly declares the value type as integer

````

- **Dynamically typed** languages infer variable types at runtime. This means once your code is run the compiler/interpreter will see your variable and its value then decide what type it is. The type is still enforced here, it just decides what the type is.
- **Dynamic Typing **is exemplified by JavaScript’s use of ‘var, const, let’ to declare variables. The compiler takes responsibility for determining the type of the value

      ```

  let a = 100 // compiler determines it is an integer

````

- Strong vs Weak Typing \* **Strong Typing** _does not_ allow different value types to interact, e.g.

          ```

  var hello = 'hello'
  hello + 17 // ERROR

````

    *   **Weak Typing** _does_ allow different value types to interact, e.g. **coercing **an integer into its string equivalent when interacting with a string

        ```

var hello = 'hello'
hello + 17 // 'hello17'

````

    *   **Weakly typed** languages allow types to be inferred as another type. For example, 1 + '2' // '12' In JS it sees you’re trying to add a number with a string — an invalid operation — so it coerces your number into a string and results in the string ‘12’.

<p id="gdcalert14" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image14.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert15">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image14.png "image_tooltip")

---

#### Primitive Types

- A **primitive **is not an object and has no methods of its own. All primitives are immutable.
- **Boolean** — true\*\* \*\*or false
- **Null** — no value
- **Undefined** — a declared variable but hasn’t been given a value
- **Number** — integers, floats, etc
- **String** — an array of characters, i.e words
- **Symbol **— a unique value that's not equal to any other value
- **Everything else is an Object type.**
- **Primitives **are wrapped in objects

      ```

  true.toString() === 'true'

````

- It works some like the below:

      ```

  Boolean(true).toString() === 'true'

````

---

### Section 2

#### Pass By Reference vs. Pass By Value

- **Pass by Value** is used with primitives

      ```

  let a = 5;
  let b = 6;
  a = 7;
  console.log(a) // 7
  console.log(b) // 6

````

- **Pass by Reference** is used with objects

      ```

  let a = {a: 1, b: 2}
  let b = a;
  a.b = 3;
  console.log(a) // {a: 1, b: 3}
  console.log(b) // {a: 1, b: 3}

````

- To **shallow clone** an object we can use **Object.assign **or the **rest operator**

      ```

  let a = {a:1, b:2}
  let b = Object.assign({}, a} // with rest operator {...a}

a.b = 3;
console.log(a) // {a:1, b:3}
console.log(b) // {a:1, b:2}

````

- To clone an array, we can use:

      ```

  let a = [1,2,3]
  let b = [].concat(a)
  a[0] = 5
  console.log(a) // [5,2,3]
  console.log(b) // [1,2,3]

````

- To **deep clone** an object we need to **stringify **and **parse **with **JSON** \* This is because of **pass by reference**, when objects are declared, a memory location, “**reference**”, is passed, rather than the object value being copied.

          ```

  let a = {a:1, b: { c: 3}}
  let deepClone = JSON.parse(JSON.stringify(a))

````

---

#### Type Coercion

- Type Coercion is the use of operators to coerce a type change in a value
- **Try to avoid type coercion as it is difficult to read and predict**

<p id="gdcalert15" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image15.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert16">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image15.png "image_tooltip")

- JavaScript provides three different value-comparison operations:
  - **===** - Strict Equality Comparison ("strict equality", "identity", "triple equals")
  - **== **- Abstract Equality Comparison ("loose equality", "double equals")
  - **Object.is** provides SameValue (new in ES2015).
- Which operation you choose depends on what sort of comparison you are looking to perform. Briefly:
  _ double equals (==) will perform a type conversion when comparing two things, and will handle NaN, -0, and +0 specially to conform to IEEE 754 (so NaN != NaN, and -0 == +0);
  _ triple equals (===) will do the same comparison as double equals (including the special handling for NaN, -0, and +0) but without type conversion; if the types differ, false is returned. \* Object.is does no type conversion and no special handling for NaN, -0, and +0 (giving it the same behavior as === except on those special numeric values).

          ```

  1 == "1" // true
  1 === 1 // false
  NaN === NaN // false

````

<p id="gdcalert16" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image16.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert17">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image16.png "image_tooltip")

[[JS Comparison Table](https://dorey.github.io/JavaScript-Equality-Table/)]

[[https://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3](https://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3)]

[[Equality comparisons and sameness - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)]

---

#### Arrays, Functions, Objects

##### Dot Notation vs. Bracket Notation

- Both can be used to access **properties **of an **object** using the **key**
- **Dot Notation** \* When working with **dot notation**, property **keys** can only be alphanumeric (and \_ and $). It can’t start with a number.

          ```

  let obj = {
  cat: 'meow',
  dog: 'woof'
  };
  let sound = obj.cat;
  console.log(sound);
  // meow

````

- **Bracket Notation** \* When working with **bracket notation**, property **keys** only have to be a **String**. They can include _any characters_, including spaces. _Variables \_may also be used \_as long as the variable resolves to a_ **String**.

          ```

  let arr = ['a','b','c'];
  let letter = arr[1];
  console.log(letter);
  // b

````

---

### The Two Pillars

#### Section 1

##### Higher Order Functions

**Higher Order Functions** are functions that take functions as parameters and/or return functions. Examples of **Higher Order Functions** can be seen in Redux.

---

##### Functions vs. Objects

- **Functions **are **callable objects**

<p id="gdcalert17" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image17.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert18">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image17.png "image_tooltip")

- **Functions **are first class citizens. **Functions **are:
  - Assignable to variables
  - Able to be passed as arguments
  - Able to be returned from functions
- Beware:
  - Initializing **functions **in loops
  - Declaring **functions **with parameters without defaults
    - **Set parameter defaults!**

---

##### Scheme + Java

---

#### Section 2

##### Closures

- **Closure** allows access to variables within its lexical scope, including the variables of parents which have been removed from the **call stack** by determining which variables will be needed by child functions and retaining them in memory.
- **Closures** are like objects in that they are a mechanism for containing **state**

      ```

  //Closure
  const closure = function() {
  let count = 0;
  return function increment() {
  count++;
  return count;
  }
  }

const incrementFn = closure()
incrementFn() //1
incrementFn() //2
incrementFn() //3

````

- Memory Efficient \* By using **closures**, we can create variables that are stored in memory to be used in the future

          ```

  const closureTest1 = (function() {
  const bigArray = new Array(7000).fill('1')
  console.log('created')
  return function(index) {
  return bigArray[index]
  }
  })()
  closureTest1(500)
  closureTest1(300)
  closureTest1(100)
  created //from console.log('created')
  //returned "1"

````

    *   A typical case without **closure **would cause the variable to be created and stored again each time it is needed. This is memory _inefficient_.

        ```

function closureTest(index) {
const bigArray = new Array(7000).fill('1')
console.log('created')
return bigArray[index]
}
closureTest(500)
closureTest(300)
closureTest(100)
created //from console.log('created')
created //from console.log('created')
created //from console.log('created')
// returned "1"

````

[[JavaScript Function Closures](https://www.w3schools.com/js/js_function_closures.asp)]

- Encapsulation
  _ **Encapsulation** allows us to hide/show properties of functions
  _ In the below example, we don’t want to expose the \_launch \_variable, so we do not return it

          ```

  const makeNuclearButton = () => {
  let timeWithoutDestruction = 0;
  const passTime = () => timeWithoutDestruction++;
  const totalPeaceTime = () => timeWithoutDestruction;
  const launch = () => {
  timeWithoutDestruction = -1;
  return '💥';
  }

setInterval(passTime, 1000);
return {totalPeaceTime}
}

const ww3 = makeNuclearButton();
ww3.totalPeaceTime()

````

[[Encapsulation in JavaScript - Software Consulting](https://www.intertech.com/Blog/encapsulation-in-javascript/)]

---

##### Prototypal Inheritance

- A prototype is a working **object** instance. Objects inherit directly from other objects.
- \***\*proto\*\*** is a reference to the parent object’s **prototype** property, e.g.

      ```

  const obj = {}
  obj.**proto** === Object.prototype // true

````

- The **prototype ** property only belongs to functions, specifically, **constructor** functions.
  - The **Object** **constructor** creates an object wrapper.
- The \***\*proto** ** and **prototype** properties are used to create a chain of **inheritance **of properties between objects, beginning with **Object** and **Primitive Types\*\*
  - **Object.create()** can be used to create **objects** with its \***\*proto** ** property linked to the **prototype **property of the object passed as **Object.create()\*\*’s argument
- **Object** is the base **function** (constructor) \* The root of everything in JavaScript is **Object** which is actually a **function**

          ```

  typeof Object //"function"

````

    *   **Object **has the property **prototype** which is the **base object** for all things in JavaScript, including JavaScript functions

        ```

typeof Object.prototype // "object"

```





---



## Object-Oriented Programming vs. Functional Programming


### OOP vs. FP


#### Object-Oriented Programming (OOP)



*   Organizing the code into units
*   An **object **is a box containing information (**state/attributes**) and operations (**methods**) that refer to the same concept, _what it is_
*   **Objects **are **first-class citizens**
*   Few operations on common data
*   Very “stateful”, we modify state
*   More **imperative**
*   Better with many _things_ and fewer _operations_


#### Functional Programming (FP)



*   A combination of functions
*   Avoiding **side-effects**
*   **Immutable **state
*   **Pure functions**
*   Functions are **first-class citizens**
*   **Composition** is more common than procedural actions, e.g. loops, iterations, and if-else
*   Manipulate data structures like trees, array, and objects
*   Performing many operations for which the data is fixed
*   Can run better in parallel processes due to fewer **side-effects**
*   More **declarative**
*   Good at processing large data for apps


### Object Oriented Programming


#### “this” keyword


```

this

````

- “**this**” is the object which the function is a property of
- “**this**” gives functions access to their object and its properties
- “**this**” helps us execute the same code for multiple objects
- “**this**” can be thought of as “who called me?” i.e., what is to the left of the dot, such as window.a()
- “**this**” is **dynamically scoped**, i.e. it doesn’t matter where it was written, it matters where it was called

<p id="gdcalert18" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image18.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert19">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image18.png "image_tooltip")

<p id="gdcalert19" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image19.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert20">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image19.png "image_tooltip")

- **Arrow functions** bind “this” to the lexical scope

<p id="gdcalert20" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image20.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert21">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image20.png "image_tooltip")

---

#### “new” keyword

- Creates a blank, plain JavaScript **object**;
- Links (sets the **constructor **of) this **object **to another **object**;
- Passes the newly created **object **from Step 1 as the **this **context;
- Returns **this **if the function doesn't return its own **object**.

---

#### “in” operator

- The **in operator** returns true if the specified property is in the specified object or its prototype chain.

####

---

#### Prototype

- A **prototype **is a working **object** instance. Objects inherit directly from other objects.
- \***\*proto\*\*** is a reference to the parent object’s **prototype** property, e.g.

      ```

  const obj = {}
  obj.**proto** === Object.prototype // true

````

- The **prototype ** property only belongs to functions, specifically, **constructor** functions.
  - The **Object** **constructor** creates an object wrapper.
- The \***\*proto** ** and **prototype** properties are used to create a chain of **inheritance **of properties between objects, beginning with **Object** and **Primitive Types\*\*
  - **Object.create()** can be used to create **objects** with its \***\*proto** ** property linked to the **prototype **property of the object passed as **Object.create()\*\*’s argument
- **Object** is the base **function** (constructor) \* The root of everything in JavaScript is **Object** which is actually a **function**

          ```

  typeof Object //"function"

````

    *   **Object **has the property **prototype** which is the **base object** for all things in JavaScript, including JavaScript functions

        ```

typeof Object.prototype // "object"

````

####

---

#### ES6 Classes

- The **class **keyword in JS is syntactic sugar. Under the hood, it still uses **prototypal inheritance**
- **Instances **of a **class **must be instantiated with the **new **keyword
- The **constructor **method is used to instantiate the **state **(data) of a new **object**
  - The **state **is typically unique to each **instance**
- Functions are typically not included in the **constructor **because it would create a memory reference for the function in each new **instance **of the **class**, thus using more memory than needed
  - By including functions as methods of the **class**, **instances **of the **class **can reference the function via the **prototype chain**
- **Prototypal Inheritance** has better memory efficiency than **classical inheritance **due to it sharing the memory references of its **prototype **properties with those **objects **that **inherit **from it. In **classical inheritance**, **instances **of the **class **create new memory references for each inherited property.

####

---

#### Java

---

#### Object.create() vs. Classes

- Both **Object.create()** and **class **are ways to create a **prototype chain**
- Some people prefer to avoid the **constructor**, **class**, and **this **keywords as much as possible to limit confusion due to **this**
- Some people prefer to use the **constructor**, **class**, and **this **keywords, perhaps because of its similarity to other languages with the Object-Oriented Programming paradigm

####

---

#### Private vs. Public vs. Protected

They are access modifiers and help us implement **Encapsulation** (or information hiding). They tell the compiler which other classes should have access to the field or method being defined.

**Private** - Only the current class will have access to the field or method.

**Protected** - Only the current class and subclasses (and sometimes also same-package classes) of this class will have access to the field or method.

**Public** - Any class can refer to the field or call the method.

####

---

#### 4 Principles of OOP

##### Encapsulation

[Encapsulation in JavaScript - Software Consulting](https://www.intertech.com/Blog/encapsulation-in-javascript/)

- **Encapsulation** allows us to hide/show properties of functions
- In the below example, we don’t want to expose the \_launch \_variable, so we do not return it

#####

---

##### Abstraction

In object-oriented programming theory, **abstraction** involves the facility to define objects that represent abstract "actors" that can perform work, report on and change their state, and "communicate" with other objects in the system. The term **encapsulation** refers to the hiding of state details, but extending the concept of data type from earlier programming languages to associate behavior most strongly with the data, and standardizing the way that different data types interact, is the beginning of **abstraction**. When **abstraction** proceeds into the operations defined, enabling objects of different types to be substituted, it is called **polymorphism**. When it proceeds in the opposite direction, inside the types or classes, structuring them to simplify a complex set of relationships, it is called **delegation** or **inheritance**.

Various object-oriented programming languages offer similar facilities for **abstraction**, all to support a general strategy of **polymorphism** in object-oriented programming, which includes the substitution of one type for another in the same or similar role. Although not as generally supported, a configuration or image or package may predetermine a great many of these bindings at compile-time, link-time, or load-time. This would leave only a minimum of such bindings to change at run-time.

[[https://en.wikipedia.org/wiki/Abstraction\_(computer_science)#Abstraction_in_object_oriented_programming](<https://en.wikipedia.org/wiki/Abstraction_(computer_science)#Abstraction_in_object_oriented_programming>)]

#####

---

##### Polymorphism

- **Polymorphism **is the provision of a single interface to entities of different types or the use of a single symbol to represent multiple different types.
- For example, given a base **class _shape_**, **polymorphism **enables the programmer to define different area **methods **for any number of derived classes, such as _circles_, _rectangles \_and \_triangles_. No matter what shape an object is, applying the area **method **to it will return the correct results.

#####

---

##### Inheritance

- **Inheritance** is the mechanism of basing an** object **or** class **upon another** object _(prototype-based inheritance) _**or **class _(class-based inheritance)_**
- The focus in **inheritance** is on _what it is_
  - Data, Methods, Functions
- Prototypal Inheritance
  - **Prototype-based programming **is a style of object-oriented programming in which behaviour reuse (known as **inheritance**) is performed via a process of* reusing existing objects* via **delegation **that serve as **prototypes**.
  - Advocates of prototype-based programming argue that it encourages the programmer to focus on the behavior of some set of examples and only later worry about classifying these objects into archetypal objects that are later used in a fashion similar to classes
- Classical Inheritance
  - **Class-based programming**, or more commonly class-orientation, is a style of Object-oriented programming (OOP) in which **inheritance **occurs via defining **classes of objects**, instead of **inheritance **occurring _via the objects alone_
  - A **class **is an extensible program-code-template for creating objects, providing initial values for state (member variables) and implementations of behavior (member functions or methods). In many languages, the **class **name is used as the name for the **class **(the template itself), the name for the default **constructor **of the class (a subroutine that creates objects), and as the **type of objects** generated by instantiating the class; these distinct concepts are easily conflated.
  - **Tight Coupling** can occur which refers to the “ripple effects” that can happen to **subclasses** (child class)\*\* **when a change is made to a **superclass \*\*(parent class)
    - **Tight Coupling **can lead to many unintended effects for the **subclasses**
    - **Tight Coupling **can help avoid repetition in code
    - The **fragile base class problem** is a fundamental architectural problem of object-oriented programming systems where base classes (**superclasses**) are considered "fragile" because seemingly safe modifications to a base class, when inherited by the derived classes, may cause the derived classes to malfunction.
      - The programmer cannot determine whether a base class change is safe simply by examining in isolation the methods of the base class.
  - The **Gorilla-Banana Problem** refers to the problem of inheriting _too much_ from **superclasses**. “You want a banana, but what you get is a gorilla holding a banana in a jungle”.
  - **Classical Inheritance** requires _excellent_ _foresight_ to avoid the problems of improper inheritance. Refactoring the structure can be a nightmare.

<p id="gdcalert21" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image21.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert22">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image21.png "image_tooltip")

---

### Functional Programming

The goal of **Functional Programming** is to _minimize **side effects**_ and compartmentalize functions so that when there is a bug, you know exactly where to go.

_An image describing the aspects of good, pure functions_

<p id="gdcalert22" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image22.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert23">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image22.png "image_tooltip")

#### Immutability

- Immutability is about not _changing_ the **state**, but rather, copying the old state, changing the new copy and _replacing_ the old **state** with the new **state**
- **Immutable objects **are simpler to construct, test, and use
  - Truly **immutable objects** are always thread-safe
  - They help to avoid **temporal coupling**
    - **Temporal coupling** is coupling that occurs when there are two or more members of a class that need to be _invoked in a particular order_
  - Their usage is **side-effect** _free_
- A **persistent data structure** is a data structure that always preserves the previous version of itself when it is modified. Such data structures are effectively **immutable**, as their operations do not (visibly) update the structure in-place, but instead always yield a new updated structure.
  - **Structural sharing** is one of the techniques used for optimizing **persistent data structures**

---

#### Idempotence

- **Idempotence** denotes predictability, i.e. given the same input, the function should always return the same output

---

#### Imperative vs. Declarative

- **Imperative code** is code that tells the machine _what to do and how to do it_
  - Machines are good with **imperative instructions**, e.g. “Please walk to the table, use your right hand to pick up the water, walk back to me and give me the water.”

_An example of imperative code_

```
for (let i = 0; i < 1000; i++) {console.log(i)}
```

- **Declarative code **is code that tells the machines _what to do and what should happen,_ it doesn’t tell the machine* how to do it*
  - Humans are good with **declarative instructions**, e.g. “Please give me that water”

_An example of declarative code_

```
[1,2,3].forEach(i => console.log(i))
```

---

#### Curry

- **Currying **transforms a function with multiple arguments into a sequence/series of functions each taking a single argument.
- **Currying** can remind us of **methods** shared through **prototypes** of objects which _saves memory_

      ```

  function multiply(a, b, c) {
  return a _ b _ c;
  }
  function multiply(a) {
  return (b) => {
  return (c) => {
  return a _ b _ c
  }
  }
  }
  log(multiply(1)(2)(3)) // 6

````

<p id="gdcalert23" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image23.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert24">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image23.png "image_tooltip")

---

#### Partial Application

- **Partial Application** is similar to **currying**
- It is a process of producing a function with a smaller number of parameters

####

---

#### Partial Application vs. Currying

- **Currying **expects _one argument at a time_
- **Partial Application** expects the _rest \_of the needed arguments on the \_second call_

####

---

#### Caching

- **Caching** is a way to store values so you can use them later

      ```

  function addTo80(n){
  console.log('simulate long computation time')
  return n + 80
  }

let cache = {}

function memoizedAddTo80(n) {
if (n in cache){
return cache[n];
} else {
console.log('simulate long computation time')
cache[n] = n + 80;
return cache[n];
}
}

````

####

---

#### Memoization

- **Memoization** is a specific kind of **caching**
  _ It **caches** a *return value* based on its parameters
  _ So, if the parameters are the same, it does a _value lookup_ instead of a running the function and calculating the _return value_ again \* Doing so can save valuable computing cycles

              ```

  function addTo80(n){
  console.log('simulate long computation time')
  return n + 80
  }

let cache = {}

function memoizedAddTo80(n) {
if (n in cache){
return cache[n];
} else {
console.log('simulate long computation time')
cache[n] = n + 80;
return cache[n];
}
}

```



_To avoid polluting the global namespace, use closures_


```

function memoizedAddTo80WithClosure(n) {
let cache = {};
return function(n){
if (n in cache){
return cache[n];
} else {
console.log('simulate long computation time')
cache[n] = n + 80;
return cache[n];
}
}
}
const memoizedAndEnclosedFunction = memoizedAddTo80WithClosure();

```



####

---



#### Pure Functions



*   A **pure function** must always return the same output given the same input
*   **Pure functions** are _easy to test_, _easy to compose_, and _avoid bugs_.
*   No **side effects**: **pure functions** cannot modify anything outside of themselves

_A function with a **side effect**, it modifies an array outside of the function_


```

const array = [1,2,3]
const mutateArray = (arr) => {
arr.pop()
}

```


_The same functionality, but with a **pure function**, i.e. no **side effects** because it creates a new array with concat() and returns the new array. It does not affect anything outside of its scope_


```

const array = [1,2,3]
const removeLastItem = (arr) => {
const newArr = [].concat(arr)
newArr.pop()
return newArr
}

````

---

#### Referential Transparency

**Referential Transparency** is generally defined as the fact that an expression, in a program, _may be replaced by its value_ (or anything having the same value) _without changing the result of the program_. This implies that methods should always return the same value for a given argument, without having any other effect.

---

#### Compose

- **Function composition **is an act or mechanism to _combine simple functions_ to build _more complicated ones_

      ```

  //Compose
  const compose = (f,g) => (data) => f(g(data))
  const multiplyBy3 = (num) => num\*3
  const makePositive = (num) => Math.abs(num)
  const multiplyBy3AndAbsolute = compose(multiplyBy3, makePositive)
  multiplyBy3AndAbsolute(-50) // 150

````

####

---

#### Pipe

- A **pipeline **consists of _a chain of processing elements_ (processes, threads, coroutines, functions, etc.), arranged so that _the output of each element is the input of the next_; the name is by analogy to a physical pipeline.

      ```

  pipe = (...fns) => x => fns.reduce((v, f) => f(v), x)

````

    ```

const pipe = (f,g) => (data) => g(f(data))
const multiplyBy3 = (num) => num\*3
const makePositive = (num) => Math.abs(num)
const multiplyBy3AndAbsolute = pipe(multiplyBy3, makePositive)
multiplyBy3AndAbsolute(-50) // 150

````

####

---

#### Pipe vs. Compose

- **compose **works exactly the same way as **pipe**, except that it applies the functions in _right-to-left order_ instead of _left-to-right_

      ```

  const pipe = (f,g) => (data) => g(f(data))

````

    ```

const compose = (f,g) => (data) => f(g(data))

````

---

### Composition vs. Inheritance

- **Inheritance** is a _top-down_ approach. It\*\* \*\*can be great with good planning and a solid, simple foundation.
  - Focuses on _what it is_
  - It can reduce repetition and be easy to read
- **Composition** is more of a _bottom-up_ approach.
  - Focuses on _what it does_
  - You can create all of the different elements needed (objects, functions, etc.) and piece them together as needed
    - It can be more difficult to follow and read
  - **Composition** can be easier to refactor and avoid side-effects
  - It requires less planning
  - The focus is on _what it has_, _what it does to data, what its abilities are_

<p id="gdcalert24" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image24.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert25">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image24.png "image_tooltip")

###

---

### Delegation

**Delegation **refers to evaluating a member (property or method) of one **object **(the receiver) in the context of another _original **object **_(the sender). **Delegation **can be done **explicitly**, _by passing the sending object to the receiving object_, which can be done in any object-oriented language; or **implicitly**, by the member lookup rules of the language, which requires language support for the feature. **Implicit delegation** is the fundamental method for behavior reuse in **prototype-based programming**, corresponding to **inheritance **in **class-based programming**. The best-known languages that support delegation at the language level are Self, which incorporates the notion of delegation through its notion of mutable parent slots that are used upon method lookup on self calls, and **JavaScript**.

##

---

## Extras

### Asynchronous JavaScript

<p id="gdcalert25" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image25.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert26">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image25.png "image_tooltip")

- APIs
- Async
- Data that we don’t have yet
- Promises

#### Web APIs

- Runs in parallel with the JS Engine inside the JS Runtime

<p id="gdcalert26" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image26.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert27">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image26.png "image_tooltip")

- Browsers are written in low-level languages for performance
  - Browsers have a JS API (Web API) to allow us to call and use browser-based functions within JS
- Storage
  - IndexedDB
- SetTimeout
  - When called, it is removed from the call stack and sent to the Web API
- Event Loop
  - Runs constantly and checks call stack
  - When a Web API function completes, it is added to the callback queue
  - When the call stack is empty, the **event loop** moves things from the callback queue to the call stack

[A visual example](http://latentflip.com/loupe/?code=ZnVuY3Rpb24gcHJpbnRIZWxsbygpIHsNCiAgICBjb25zb2xlLmxvZygnSGVsbG8gZnJvbSBiYXonKTsNCn0NCg0KZnVuY3Rpb24gYmF6KCkgew0KICAgIHNldFRpbWVvdXQocHJpbnRIZWxsbywgMzAwMCk7DQp9DQoNCmZ1bmN0aW9uIGJhcigpIHsNCiAgICBiYXooKTsNCn0NCg0KZnVuY3Rpb24gZm9vKCkgew0KICAgIGJhcigpOw0KfQ0KDQpmb28oKTs%3D!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D) of the Call Stack and the Web API in action

- DOM
- fetch
- Asynchronous

####

---

#### Callbacks

A **callback **function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

Here is a quick example:

```
function greeting(name) {
  alert('Hello ' + name);
}
function processUserInput(callback) {
  var name = prompt('Please enter your name.');
  callback(name);
}
processUserInput(greeting);
```

The above example is a **synchronous callback**, as it is executed immediately.

Note, however, that **callbacks **are often used to continue code execution after an asynchronous operation has completed — these are called **asynchronous callbacks**. A good example is the **callback **functions executed inside a **.then()** block chained onto the end of a **promise **after that **promise **fulfills or rejects. This structure is used in many modern web APIs, such as **fetch()**.

[[Callback function - MDN Web Docs Glossary: Definitions of Web-related terms](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function)]

_Callback examples_

```
el.addEventListener("click", submitForm);
```

```
//Callback pyramid of doom

movePlayer(100, "Left", function(){
	movePlayer(400, "Left", function(){
		movePlayer(10, "Right", function(){
			movePlayer(330, "Left", function(){
			})
		})
	})
})
```

```
grabTweets('twitter/andreineagoie', (error, andreiTweets) => {
	if(error){
		throw Error;
	}
	displayTweets(andreiTweets)
	grabTweets('twitter/elonmusk', (error, elonTweets) => {
		if(error){
			throw Error;
		}
		displayTweets(elonTweets)
		grabTweets('twitter/vitalikbuterin', (error, vitalikTweets) => {
			if(error){
				throw Error;
			}
			displayTweets(vitalikTweets)
		})
	})
})
```

####

---

#### Promises

- Before **promises**, there were **callbacks**.
- A **promise** is an **object** that may produce a single value some time in the future
  - Resolved
  - Rejected
  - Pending
- **.catch()** can be used to catch any errors thrown in front of the **.catch()** in a promise chain

_An example of Promise_

```
//Promise
movePlayer(100, 'Left')
	.then(() => movePlayer(400, "Left"))
	.then(() => movePlayer(10, "Right"))
	.then(() => movePlayer(330, "Left"))
```

```
const promise = new Promise((resolve, reject) => {
	if(true) {
		resolve("stuff worked");
	}else{
		reject("Error, it broke)")
	}
})
promise.then(result => console.log(result)) //stuff worked

// promise chain
promise
	.then(result => result + "!")
	.then(result2 => console.log(result2)) //stuff worked!
promise
	.then(result => result + "!")
	.then(result2 => {
		throw Error
		console.log(result2)
	})
	.catch(() => console.log('Error!')) // Error!
```

```
new Promise(function(resolve, reject) {

  setTimeout(() => resolve(1), 1000); // (*)

}).then(function(result) { // (**)

  alert(result); // 1
  return result * 2;

}).then(function(result) { // (***)

  alert(result); // 2
  return result * 2;

}).then(function(result) {

  alert(result); // 4
  return result * 2;

});
```

- The whole thing works, because a call to **promise.then** returns a **promise**, so that we can call the next **.then** on it.
- When a handler returns a value, it becomes the result of that **promise**, so the next **.then **is called with it.

[[Promises chaining](https://javascript.info/promise-chaining)]

##### Promise.all()

- **Promise.all()** takes an array of promises and returns their values when all promises are resolved, or throws an error.

<table>
  <tr>
   <td>
<code>const promise1 = new Promise((resolve, reject) => { \
   if (true){ \
       resolve('promise1') \
   }else{ \
       reject('Error, it broke') \
   } \
}) \
 \
const promise2 = new Promise((resolve, reject) => { \
   setTimeout(resolve, 100, 'promise2') \
}) \
 \
const promise3 = new Promise((resolve, reject) => { \
   setTimeout(resolve, 2000, 'promise3') \
}) \
 \
const promise4 = new Promise((resolve, reject) => { \
   setTimeout(resolve, 5000, 'promise4') \
}) \
 \
Promise.all([promise1, promise2, promise3, promise4]).then((values) => { \
   console.log(values) /*after 5000ms, logs ["promise1", "promise2",      "promise3", "promise4"] */ \
}) </code>
   </td>
  </tr>
  <tr>
   <td>
   </td>
  </tr>
</table>

_An example use for Promise.all()_

```
const urls = [
 "https://jsonplaceholder.typicode.com/users",
 "https://jsonplaceholder.typicode.com/posts",
 "https://jsonplaceholder.typicode.com/albums",
];


Promise.all(
  urls.map(url => {
    return fetch(url).then(resp => resp.json());
  })
).then(results => {
  results.map(result => console.log(result))
});
```

####

---

#### Async/Await

- **async **and **await** are syntactic sugar on top of **Promises**

_A normal Promise-based fetch()_

```
fetch("https://jsonplaceholder.typicode.com/users")
 .then(resp => resp.json())
 .then(console.log);
```

_An async/await-styled fetch()_

```
async function fetchUsers() {
 const response = await    fetch("https://jsonplaceholder.typicode.com/users");
 const data = await response.json();
 console.log(data);
}

fetchUsers()
```

_An async/await-styled Promise.all() with try/catch_

```
const urls = [
 "https://jsonplaceholder.typicode.com/users",
 "https://jsonplaceholder.typicode.com/posts",
 "https://jsonplaceholder.typicode.com/albums",
];

const getData = async function() {
 try {
   const [users, posts, albums] = await Promise.all(
     urls.map(url => {
       return fetch(url).then(resp => resp.json());
     })
   );
   console.log(users);
   console.log(posts);
   console.log(albums);
 } catch (err) {
   console.log(err);
 }
};
getData();
```

##### .finally()

- **.finally() **runs code after a **promise **whether it succeeds or fails

      ```

  const urls = [
  "https://jsonplaceholder.typicode.com/users",
  "https://jsonplaceholder.typicode.com/posts",
  "https://jsonplaceholder.typicode.com/albums",
  ];

Promise.all(
urls.map(url => {
return fetch(url).then(resp => resp.json());
})
)
.then(results => {
console.log(results[0]);
console.log(results[1]);
console.log(results[2]);
})
.catch(err => console.log(err))
.finally(() => console.log("finally"));

```




##### for await of


```

const urls = [
"https://jsonplaceholder.typicode.com/users",
"https://jsonplaceholder.typicode.com/posts",
"https://jsonplaceholder.typicode.com/albums",
];
const getData2 = async function() {
const arrayofPromises = urls.map((url) => fetch(url));
for await (let request of arrayofPromises) {
const data = await request.json();
console.log(data);
}
}

```



####

---



#### Microtask Queue (Job Queue)



*   The **event loop** checks the **job queue** before the **callback queue**, the **job queue** has _higher priority._
*   The **job queue** is for **Promises**



<p id="gdcalert27" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image27.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert28">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image27.png "image_tooltip")




<p id="gdcalert28" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image28.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert29">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image28.png "image_tooltip")




*   Some older browsers may not have a **job queue** yet, so do not rely on it too much.


####

---



#### Task Queue (Callback Queue)


####

---



#### Event Loop



*   Runs constantly and checks call stack
*   When a Web API function completes, it is added to the callback queue
*   When the call stack is empty, the **event loop** moves things from the callback queue to the call stack
*   [A visual example](http://latentflip.com/loupe/?code=ZnVuY3Rpb24gcHJpbnRIZWxsbygpIHsNCiAgICBjb25zb2xlLmxvZygnSGVsbG8gZnJvbSBiYXonKTsNCn0NCg0KZnVuY3Rpb24gYmF6KCkgew0KICAgIHNldFRpbWVvdXQocHJpbnRIZWxsbywgMzAwMCk7DQp9DQoNCmZ1bmN0aW9uIGJhcigpIHsNCiAgICBiYXooKTsNCn0NCg0KZnVuY3Rpb24gZm9vKCkgew0KICAgIGJhcigpOw0KfQ0KDQpmb28oKTs%3D!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D) of the Call Stack and the Web API in action


####

---



#### Parallel, Sequence, and Race


##### Parallel

**Parallel** means to run multiple **promises** in **parallel**, beginning together and returning them all when they are all finished.


```

const promisify = (item, delay) =>
new Promise(resolve => setTimeout(() => resolve(item), delay));

// functions that return promises
const a = () => promisify("a", 100);
const b = () => promisify("b", 5000);
const c = () => promisify("c", 3000);
console.log(a,b,c) // [Function] [Function] [Function]
console.log(a(),b(),c()) // Promise {} Promise {} Promise {}
async function parallel() {
const promises = [a(), b(), c()];
const [output1, output2, output3] = await Promise.all(promises);
return `parallel is done: ${output1} ${output2} ${output3}`;
}
parallel().then(console.log) // parallel is done: a b c

```



##### Sequence

**Sequence** means that each **promise** will _wait for earlier promises to resolve _before beginning.


```

const promisify = (item, delay) =>
new Promise(resolve => setTimeout(() => resolve(item), delay));

// functions that return promises
const a = () => promisify("a", 100);
const b = () => promisify("b", 5000);
const c = () => promisify("c", 3000);
console.log(a,b,c) // [Function] [Function] [Function]
console.log(a(),b(),c()) // Promise {} Promise {} Promise {}
async function sequence() {
const output1 = await a();
const output2 = await b();
const output3 = await c();
return `sequence is done: ${output1} ${output2} ${output3}`;
}

sequence().then(console.log) // sequence is done: a b c

```



##### Race

**Race** means that _the first **promise** to resolve will be returned_ and the others will be ignored.


```

const promisify = (item, delay) =>
new Promise(resolve => setTimeout(() => resolve(item), delay));

// functions that return promises
const a = () => promisify("a", 100);
const b = () => promisify("b", 5000);
const c = () => promisify("c", 3000);
console.log(a,b,c) // [Function] [Function] [Function]
console.log(a(),b(),c()) // Promise {} Promise {} Promise {}
async function race() {
const promises = [a(), b(), c()]
const output1 = await Promise.race(promises);
return `race is done: ${output1}`
}

race().then(console.log) // race is done: a

```



#### Threads, Concurrency, and Parallelism

_An example of multithreading/parallelism in Node.js, generates a new thread_


```

const {spawn} = require('child_process')

spawn('git', ['stuff'])

````

- **Concurrency** means multiple computations are happening at the same time.

[[Concurrency in JavaScript.. Learn how to write asynchronous… | by Onejohi](https://medium.com/@onejohi/concurrency-in-javascript-f5bb387708d8)]

<p id="gdcalert29" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image29.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert30">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image29.png "image_tooltip")

##### Web Workers

<p id="gdcalert30" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image30.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert31">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image30.png "image_tooltip")

####

---

### Error Handling

- Errors are used with the keyword **throw**
- The **name** property refers to the general class of **Error**
- The **message **property generally provides a more succinct message than one would get by converting the error object to a string.
- The **stack** property traces the **Error**’s position in the call-stack back to the global context which is typically `&lt;anonymous>`

      ```

  const c = new Error('again?')
  console.log(c.name) // Error
  console.log(c.message) // again?
  console.log(c.stack) // Error: again?↵ at <anonymous>:1:11

````

- The below example shows the **stack** property at work.
- First, the class of **Error **is given “Error”,
- Then the **message**, “what??”,
- Finally the **stack** trace “at a (&lt;anonymous>:2:13)↵at &lt;anonymous>:5:1:5:1”, meaning the first context is the function “a” and the second context is anonymous (global context)

      ```

  function a() {
  const b = new Error('what??')
  return b
  }
  a().stack // Error: what??↵at a (<anonymous>:2:13)↵at <anonymous>:5:1:5:1

````

- **Error** types
  - **Error**, general error
  - **SyntaxError**, e.g. a misplaced comma
  - **ReferenceError**, e.g. undefined variable
- When an **Error** is thrown, it searches up the call-stack for a **catch**.
- If no **catch** is found, the **runtime** handles it
- In the browser, it is **onerror()**
- In Node.js, it is **process.on(‘uncaughtException’)**

<p id="gdcalert31" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image31.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert32">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image31.png "image_tooltip")

#### try/catch/finally

- **try/catch** blocks can be used to handle \_synchronous\*\* \*\*\_code

      ```

  function fail() {
  try {
  console.log("this works");
  } catch (error) {
  console.log("oops, error");
  }
  }

````

    ```

function fail() {
try {
consol.log("this works"); //misspelled "console" as "consol"
} catch (error) {
console.log("oops, error"); //throws an error, "oops, error ReferenceError"
}
}

````

    ```

function fail() {
try {
console.log("this works"); //successfully logs because it is above the error
throw new Error('whoops!') //throws an error, looks for a catch
} catch (error) {
console.log("We have an error", error); // "We have an error Error: whoops!
}
}

````

_finally_

```
function fail() {
 try {
   console.log("this works"); //successfully logs because it is above the error
   throw new Error("whoops!"); //throws an error, looks for a catch
 } catch (error) {
   console.log("We have an error", error); // "We have an error Error: whoops!
 } finally {
   console.log("final"); // logs "final" regardless of try/catch success/fail
 }
}
```

#### Errors in asynchronous code

- **Promises** use the **.catch()** method to catch errors
- Without a **.catch()** a **Promise** _can fail silently_, meaning no **Error** is shown despite there being one

_This Promise **fails silently**, it does not produce an error message_

```
Promise.resolve("asyncfail")
 .then(response => {
   throw new Error("#1 fail");
   return response;
 })
 .then(response => {
   console.log(response);
 });
```

_This promise fails and **does** produce an error via **.catch()**_

```
Promise.resolve("asyncfail")
 .then(response => {
   throw new Error("#1 fail");
   return response;
 })
 .then(response => {
   console.log(response);
 })
 .catch(error => console.log(error));
```

_A **.catch()** can return and use a **.then()** to further process the return from the **.catch()**_

```
Promise.resolve("asyncfail")
 .then(response => {
   throw new Error("#1 fail");
   return response;
 })
 .then(response => {
   console.log(response);
 })
 .catch(error => {
   return error;
 })
 .then(response => {
   console.log(response.message); // #1 fail
 });
```

**_.catch() can be chained. In this example, the “#1 fail” Error occurs, which is caught in the first .catch(), the first .catch() throws a new Error which is then caught by the second .catch() which then console.logs “final error”_**

```
Promise.resolve("asyncfail")
  .then(response => {
    throw new Error("#1 fail");
    return response;
  })
  .then(response => {
    console.log(response);
  })
  .catch(error => {
    throw new Error("#2");
  })
  .then(response => {
    console.log(response.message);
  })
  .catch(error => {
    console.log("final error"); // final error
  });
```

- With nested **Promises**, it is important to have a **.catch()** nested with the **Promise** as well, otherwise, the errors are not handled correctly

_Nested **Promise**’s error is not handled correctly_

```
Promise.resolve("asyncfail")
 .then(response => {
   Promise.resolve().then(() => {
     throw new Error("#3 fail");
   }); //should have .catch() here
   return 5;
 })
 .then(response => {
   console.log(response);
 })
 .then(response => {
   console.log(response.message);
 })
 .catch(error => {
   console.log("final error");
 });
```

##### async/await Error Handling

- While **async/await** is _asynchronous_, it looks like and is handled like \_synchronous \_code. This means that **try/catch** blocks work for **async/await**.

      ```

  (async function() {
  try {
  await Promise.resolve("#1 yeah");
  await Promise.reject("#2 no");
  } catch (error) {
  console.log(error);
  }
  })();

````

#### Custom Errors

- **Error** is a class and can be \_extended \_with the **extends** keyword to create **custom Errors**.
- This can be useful for creating **secure Errors* by not displaying too much information.***

      ```

  class DatabaseError extends Error {
  constructor(message) {
  super(message);
  this.name = "DatabaseError";
  }
  }
  class PermissionError extends Error {
  constructor(message) {
  super(message);
  this.name = "PermissionError";
  }
  }

class AuthenticationError extends Error {
constructor(message) {
super(message);
this.name = "AuthenticationError";
this.favoriteSnack = "grapes";
}
}
const a = new AuthenticationError("snack");
console.log(a.favoriteSnack); // grapes
throw new AuthenticationError("oops"); // AuthenticationError: oops

````

---

### Destructuring

Destructuring allows us to remove values from the enclosing structure of arrays and objects, you can think of it as removing the `[]` or `{}`.

_Array destructuring_

```
const sampleArray = [1,2,3]
const [one, two, three] = sampleArray
console.log(one, two, three) // 1 2 3
```

_Object destructuring_

```
const sampleObject = {one: 1, two: 2, three: 3}
const {one, two, three} = sampleObject
console.log(one, two, three) // 1 2 3
```

#### Renaming destructured object properties

We can **rename** _object properties_ while destructuring objects, but not arrays, of course, as arrays have _elements_ with _indices_ and not _property names (keys)._

\_Here the property name <code>one</code> is changed to <code>newName</code> during destructuring by appending <code>: newName</code> to <code>one</code></em>

```
const sampleObject = {one: 1, two: 2, three: 3}
const {one: newName, two, three} = sampleObject
console.log(newName, two, three) // 1 2 3
console.log(one) // Uncaught ReferenceError: one is not defined
```

####

---

### JavaScript’s “...” operator

_This section needs some clarification and additional examples_

#### Spread Operator

A spread operator _spreads_, or separates, the values contained in an object or array.

```
var myName = ["Marina" , "Magdy" , "Shafiq"];
var newArr = [...myName ,"FrontEnd" , 24];
console.log(newArr) ; // ["Marina" , "Magdy" , "Shafiq" , "FrontEnd" , 24 ] ;
```

[Source](https://medium.com/javascript-in-plain-english/es6-spread-parameter-vs-rest-operator-5e3c924c4e1f)

_Here the spread operator separates the values of the array into the parameter_

```
const array = [1,2,3,4,5]
function sum(a,b,c,d,e){
   return a+b+c+d+e
}
sum(...array) // 15
```

#### Rest Pattern

The **rest pattern** is used to _collect extra values_ beyond those explicitly defined.

##### Rest Parameter

A **rest parameter** is used to collect _the **rest **of the arguments_ into a single parameter as an array. A **rest parameter** must be the last parameter.

```

```

##### Rest Destructuring

**Rest destructuring** is very similar to the rest parameter in that it is used to collect the **rest** of the values into an array.

_A rest parameter being used in deconstructing an array: const [one, **...rest**] = array_

```
const array = [1,2,3]
const [one, ...rest] = array
one // 1
rest // [2,3]
```

_An object rest destructuring _

```
const animals ={
    tiger: 23,
    lion: 5,
    monkey: 2
}

const {tiger, ...rest} = animals

function objectSpread(p1,p2){
   console.log(p1)
   console.log(p2)
}

objectSpread(tiger, rest)
// 23
// {lion: 5, monkey: 2}
```

#### Spread and Rest together

```
function makeArray(arg1, ...args){ //a rest parameter collects extra values
   console.log(arg1) // 1
   console.log(args) // [2,3,4,5,6,7]
   console.log(arg1, ...args) // 1,2,3,4,5,6,7 via spread operator
   return [arg1, ...args] // [1,2,3,4,5,6,7] via spread operator
}
makeArray(1, 2, 3, 4, 5, 6, 7) // all arguments besides the first are      // collected by ...args
```

####

---

### Modules in JavaScript

**Modules** in JavaScript allows us to _containerize_ our JavaScript. It helps us to interact with other code and _avoid polluting the global namespace_.

####

---

#### Module Pros and Cons

- Pros
  - Limits global namespace pollution
  - API remaining the same, work on **modules **can be done independently of each other
- Cons
  - Obscures dependencies

####

---

#### IIFE

- Before **modules**, JavaScript used **IIFE **to create a _module pattern_ to _containerize_ our code.
- An **IIFE **would create a **function scope** for the functions and variables to live inside of where they would be **private**. This would _prevent pollution of the global namespace_.
- By returning functions/variables from the **IIFE** in an object, we create an **interface **for interacting with the code inside of the **IIFE** **function scope**.
- This method of _containerizing_ our code is called the **Revealing Module Pattern.**

_Functions and variables become private to the fightModule function scope_

```
//IIFE
//Module Pattern
 var fightModule = (function () {
   var harry = 'potter'
   var voldemort = 'He who must not be named'

   function fight(char1, char2) {
     var attack1 = Math.floor(Math.random() * char1.length);
     var attack2 = Math.floor(Math.random() * char2.length);
     return attack1 > attack2 ? `${char1} wins` : `${char2} wins`;
   }
   return {
     fight: fight
   }
 })()
```

_Creates an interface_

```
return {
     fight: fight
   }
```

####

---

#### Native ES Modules

- Brought to client-side JavaScript in ES6
- Coming soon to Node.js
- Provides native module functionality in the browser

      ```

  //Native ES6 Modules
  import module1 from 'module1' //{fight};
  import module2 from 'module2' //importedFunc2

export function jump() {
}

````

- When using modules in **script **tags, the **type** attribute should be **module**.
- When using **modules**, CORS policy applies and they must be served from a server proxy, e.g. [live-server](https://www.npmjs.com/package/live-server)

<p id="gdcalert32" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image32.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert33">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image32.png "image_tooltip")

Default and named exports

####

---

#### CommonJS

- Created for server-side coding
- Still used by Node.js
- **Modules **are loaded _synchronously_

  ```
  //CommonJS and AMD
  var module1 = require('module1') //.fight
  var module2 = require('module2') //importedFunc2
  ```

function fight(){

}

module.exports ={
fight: fight
}

````

- **Browserify** bundles all scripts in a single bundle.js while understanding the module syntax and maintaining separation

####

---

#### UMD

**UMD** (Universal Module Definition) is essentially an if/else that determines whether to use **AMD ** or **CommonJS**

####

---

#### AMD

**AMD** (Asynchronous Module Definition) is an alternative to **CommonJS** for creating modules in JavaScript

```
//AMD
define(["module1", "module2"], function(module1Import, module2Import) {
 var module1 = module1Import; //.fight
 var module2 = module2Import; //importedFunc2

 function dance() {}
 return {
   dance: dance,
 };
});
```

### Template Literals

**Template literals** let you do more with **strings.**

```
const templateLiteral = `I am a template literal`
```

#### Multi-line strings

**Template literals** let you write multi-line strings

```
const templateLiteral = `I am a very long multi-line
template literal`
console.log(templateLiteral) // I am a very long multi-line
				  //template literal
```

#### Avoid escaping characters

**Template literals** can help you avoid some annoying features of normal strings.

_This line of code will throw an error because the single-quotes used to enclose the string are being interrupted by the apostrophe used in the word “**I’m**”_

```
const annoyingString = 'I'm really annoying'
```

_You would need to write it this way:_

```
const annoyingString = "I'm really annoying"
```

The same is true of strings using double-quotes

```
const annoyingString2 = "don't try to quote anyone here: "He said he would be there""
```

_You would need to write it this way:_

```
const annoyingString2 = "don't try to quote anyone here: 'He said he would be there'"
```

Thankfully, **template literals** help us solve this problem:

```
const lovelyTemplateLiterals = `"It's so easy to use apostrophes and quote people", he said`
```

#### Variable Insertion

Template literals are great for inserting the value of a variable into a string using the `${}` pattern

```
const myVariable = 10
const insertedVariable = `I can see ${myVariable} elephants` // "I can see 10 elephants"
```

##### Avoid String concatenation

With traditional strings, we had to insert variables and concatenate (add together) strings this way

```
const myVariable = "String2"
const stringCat = "String1 " + myVariable + " String3" // "String1 String2 String3"
```

```
const firstName = "foo"
const lastName = "bar"
const fullName = firstName + " placeholder " + lastName // "foo placeholder //bar"
```

### Semicolons

A semi-colon `;` is used to end a line of code.

You may have noticed that there are not always semi-colons written at the end of a line of code. That’s because the JS interpreter is able to intelligently determine where a semi-colon should be placed. _However,_ it does not always put the semi-colon where you might expect or want.

### Iterators

### Generator

### Symbols

### Map

A `Map `is similar to an `Object `in most cases. The primary difference is that a `Map `can use any type as a key.

<table>
  <tr>
   <td>
   </td>
   <td><strong>Map</strong>
   </td>
   <td><strong>Object</strong>
   </td>
  </tr>
  <tr>
   <td><strong>Accidental keys</strong>
   </td>
   <td>A <code>Map</code> does not contain any keys by default. It only contains what is explicitly put into it.
   </td>
   <td>An <code>Object</code> has a prototype, so it contains default keys that could collide with your own keys if you're not careful.
<p>
<strong>Note:</strong> As of ES5, this can be bypassed by using <code><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create">Object.create(null)</a></code>, but this is seldom done.
   </td>
  </tr>
  <tr>
   <td><strong>Key types</strong>
   </td>
   <td>A <code>Map</code>'s keys can be any value (including functions, objects, or any primitive).
   </td>
   <td>The keys of an <code>Object</code> must be either a <code><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a></code> or a <code><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol">Symbol</a></code>.
   </td>
  </tr>
  <tr>
   <td><strong>Key order</strong>
   </td>
   <td>The keys in <code>Map</code> are ordered. Thus, when iterating over it, a <code>Map</code> object returns keys in order of insertion.
   </td>
   <td>The keys of an <code>Object</code> are not ordered.
<p>
<strong>Note:</strong> Since ECMAScript 2015, objects <em>do</em> preserve creation order for string and <code>Symbol</code> keys. In JavaScript engines that comply with the ECMAScript 2015 spec, iterating over an object with only string keys will yield the keys in order of insertion.
   </td>
  </tr>
  <tr>
   <td><strong>Size</strong>
   </td>
   <td>The number of items in a <code>Map</code> is easily retrieved from its <code><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/size">size</a></code> property
   </td>
   <td>The number of items in an <code>Object</code> must be determined manually
   </td>
  </tr>
  <tr>
   <td><strong>Iteration</strong>
   </td>
   <td>A <code>Map</code> is an <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/iterable">iterable</a>, so it can be directly iterated
   </td>
   <td>Iterating over an <code>Object</code> requires obtaining its keys in some fashion and iterating over them
   </td>
  </tr>
  <tr>
   <td><strong>Performance</strong>
   </td>
   <td>Performs better in scenarios involving frequent additions and removals of key-value pairs
   </td>
   <td>Not optimized for frequent additions and removals of key-value pairs
   </td>
  </tr>
</table>

[Map - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)

### WeakMap

- A `WeakMap` is essentially a `Map`, but the keys are more ephemeral.
- Keys of WeakMaps are of the type `Object` only. [Primitive data types](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) as keys are not allowed (e.g. a <code>[Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)</code> can't be a <code>WeakMap</code> key)

  By contrast, native <code>WeakMap</code>s hold "weak" references to key objects, which means that they do not prevent garbage collection in case there would be no other reference to the key object. This also avoids preventing garbage collection of values in the map. Native WeakMaps can be particularly useful constructs when mapping keys to information about the key that is valuable only if the key has not been garbage collected.

[WeakMap - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)

### Set

`Set` objects are collections of values. You can iterate through the elements of a set in insertion order. A value in the `Set` **may only occur once**; it is unique in the `Set`'s collection.

[Set - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)

####

---

### Proxy

_I have decided to add this section, which was not included in Advanced JavaScript Concepts particularly for its ability to implement private properties in objects._

    JavaScript proxies have the ability to change the fundamental behavior of objects and functions. We can extend the language to better suit our requirements or simply use it for things like validation and access control on a property.


    Until proxies were introduced, we did not have native level access to change the fundamental behavior of an object, nor a function. But with them, we have the ability to act as a middle layer, to change how the object should be accessed, generate information such as how many times a function has been called, etc.

_Implementing a plain object literal_

```
const person = {
    firstName: 'John',
    lastName: 'Doe',
};
```

_The handler allows us to define behavior for the objects, e.g. get/set_

```
const handler = {
    get(target, property) {
        console.log(`you have read the property ${property}`);
        return target[property];
    }
};
```

```
const proxyPerson = new Proxy(person, handler);

console.log(proxyPerson.firstName);
// you have read the property firstName
// John
console.log(proxyPerson.lastName);
// you have read the property lastName
// Doe
```

    As you may already know, JavaScript doesn't support private properties. So sometimes as a convention, developers use the underscore (_) in front of the property name, for example, _securityNumber, to identify it as a private property.


    However, this does not actually enforce anything in the code level. Developers just know they should not directly access the properties that start with _. With proxies, we can change that.

_Implementing private property_

```
const person = {
    firstName: 'John',
    lastName: 'Doe',
    age: 21,
    _ssn: '123-45-6789'
};
```

```
const handler = {
    get(target, property) {
        if (property[0] === '_') {
            throw new Error(`${property} is a private property`);
        }

        return target[property];
    }
}

const proxyPerson = new Proxy(person, handler);

console.log(proxyPerson._ssn);
// Error: _ssn is a private property
```

_We are not limited to implementing private properties, we can implement rules and type-safety_

```
const handler = {
    set(target, property, value) {
        if (property === 'age') {
            if (!(typeof value === 'number')) {
                throw new Error('Age should be a number');
            }

            if (value < 0 || value > 150) {
                throw new Error("Age value should be in between 0 and 150");
            }
        }

        target[property] = value;
    }
};

const proxyPerson = new Proxy(person, handler);
proxyPerson.age = 170;
// Error: Age value should be in between 0 and 150
```

[[Introduction to JavaScript Proxies in ES6](https://stackabuse.com/introduction-to-javascript-proxies-in-es6/)]

####

---

This document has been created as a supplement to the Udemy course [Advanced JavaScript Concepts](https://www.udemy.com/advanced-javascript-concepts/) by [Andrei Neagoie](https://github.com/aneagoie). In addition to the information from Andrei Neagoie, information and images have been compiled from many different sources around the internet. I do not claim ownership of anything in this document and seek to correctly attribute all information. When no source is given, it can be assumed that the information comes from Andrei Neagoie’s course. Compiled by [Bryan Windsor](https://github.com/taidaid).

<p id="gdcalert33" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image33.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert34">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image33.png "image_tooltip")

<p id="gdcalert34" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image34.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert35">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image34.png "image_tooltip")

<p id="gdcalert35" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image35.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert36">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image35.png "image_tooltip")

```

```

```

```
