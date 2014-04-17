---
layout: post
title: JavaScript Code Style Guide
---

## Resources

* [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwldrn/idiomatic.js)
* [JavaScript Style Guides And Beautifiers](http://addyosmani.com/blog/javascript-style-guides-and-beautifiers/)
* [Front-end Code Standards & Best Practices](http://isobar-idev.github.io/code-standards/)
* [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
* [Your code sucks, let's fix it - PHP Master Series 2012](http://www.slideshare.net/rdohms/your-code-sucks-lets-fix-it-php-master-series-2012)

## JavaScript Style Rules

### Naming

#### General rules

* functionNamesLikeThis
* variableNamesLikeThis
* ClassNamesLikeThis
* EnumNamesLikeThis
* methodNamesLikeThis
* CONSTANT_VALUES_LIKE_THIS
* foo.namespaceNamesLikeThis.bar

#### Namespaces

_ALWAYS_ prefix identifiers in the global scope with a unique pseudo namespace related to the project or library.

Alias long type names to improve readability

    function() {
        var MyClass = some.long.namespace.MyClass;
        var staticHelper = some.long.namespace.MyClass.staticHelper;
        staticHelper(new MyClass());
    }

#### Filenames

Filenames should be all lowercase in order to avoid confusion on case-sensitive platforms.

    foo-bar-test.js

### Custom toString() methods

* always succeeds
* does not have side-effects

### Deferred initialization

It isn't always possible to initialize variables at the point of declaration, so deferred initialization is fine.

### Explicit scope

Always use explicit scope - doing so increases portability and clarity.

### Code formatting

#### Curly Braces

Because of implicit semicolon insertion, always start your curly braces on the same line as whatever they're opening. For example:

    if (something) {
        // ...
    } else {
        // ...
    }

#### Array and Object Initializers

Single-line array and object initializers are allowed when they fit on a line:

    var arr = [1, 2, 3];  // No space after [ or before ].
    var obj = {a: 1, b: 2, c: 3};  // No space after { or before }.

Multiline array initializers and object initializers are indented 4 spaces, with the braces on their own line, just like blocks.

    // Object initializer.
    var inset = {
        top: 10,
        right: 20,
        bottom: 15,
        left: 12
    };

    // Array initializer.
    var users = [
        "Robin",
        "Terry",
        "Ford",
        "Arthur",
        "Marvin"
    ];

    // Used in a method call.
    goog.dom.createDom(goog.dom.TagName.DIV, {
        id: "foo",
        className: "some-css-class",
        style: "display:none"
    }, "Hello, world!");

Long identifiers or values present problems for aligned initialization lists, so always prefer non-aligned initialization. For example:

    CORRECT_Object.prototype = {
        a: 0,
        b: 1,
        lengthyName: 2
    };

Not like this:

    WRONG_Object.prototype = {
        a          : 0,
        b          : 1,
        lengthyName: 2
    };

#### Function Arguments

    // Eight-space, one argument per line. Works with long function names,
    // survives renaming, and emphasizes each argument.
    goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
            veryDescriptiveArgumentNumberOne,
            veryDescriptiveArgumentTwo,
            tableModelEventHandlerProxy,
            artichokeDescriptorAdapterIterator) {
        // ...
    };

#### Passing Anonymous Functions

    prefix.something.reallyLongFunctionName("whatever", function(a1, a2) {
        if (a1.equals(a2)) {
            someOtherLongFunctionName(a1);
        } else {
            andNowForSomethingCompletelyDifferent(a2.parrot);
        }
    });

#### Binary and Ternary Operators

Always put the operator on the preceding line, so that you don't have to think about implicit semi-colon insertion issues. Otherwise, line breaks and indentation follow the same rules as in other Google style guides.

    var x = a ? b : c;  // All on one line if it will fit.

    // Indentation +4 is OK.
    var y = a ?
        longButSimpleOperandB : longButSimpleOperandC;

    // Indenting to the line position of the first operand is also OK.
    var z = a ?
            moreComplicatedB :
            moreComplicatedC;

This includes the dot operator.

    var x = foo.bar().
        doSomething().
        doSomethingElse();

### Strings

Prefer `"` over `'`.

## JavaScript Language Rules

### var

_ALWAYS_ use `var`.

### Constants

* Use `NAMES_LIKE_THIS` for constant values.
* Use @const to indicate a constant pointer.
* Never use the `const` keyword as it not supported in Internet Explorer.

### Semicolons

_ALWAYS_ use semicolons.

Relying on implicit insertion can cause subtle, hard to debug problems. Don't do it. You're better than that.

Example 1:

    MyClass.prototype.myMethod = function() {
        return 42;
    }  // No semicolon here.

    (function() {
        // Some initialization code wrapped in a function to create a scope for locals.
    })();

Result: JavaScript error - first the function returning 42 is called with the second function as a parameter, then the number 42 is "called" resulting in an error.

    MyClass.prototype.myMethod = function() {
        return 42;
    }(function() {
        // Some initialization code wrapped in a function to create a scope for locals.
    })();

Example 2:

    var x = {
        i: 1,
        j: 2
    }  // No semicolon here.

    // Trying to do one thing on Internet Explorer and another on Firefox.
    // I know you'd never write code like this, but throw me a bone.
    [normalVersion, ffVersion][isIE]();

Result: You will most likely get a 'no such property in undefined' error at runtime as it tries to call `x[ffVersion][isIE]()`.

    var x = {
        i: 1,
        j: 2
    }[normalVersion, ffVersion][isIE]();


Example 3:

    var THINGS_TO_EAT = [apples, oysters, sprayOnCheese] // No semicolon here.

    // conditional execution a la bash
    -1 == resultOfOperation() || die();

Result: `die` is called unless `resultOfOperation()` is `NaN` and `THINGS_TO_EAT` gets assigned the result of `die()`.

    var THINGS_TO_EAT = [apples, oysters, sprayOnCheese]-1 == resultOfOperation() || die();


### Function Declarations Within Blocks

Do not do this:

    if (x) {
        function foo() {}
    }

While most script engines support Function Declarations within blocks it is not part of ECMAScript (see ECMA-262, clause 13 and 14). Worse implementations are inconsistent with each other and with future EcmaScript proposals. ECMAScript only allows for Function Declarations in the root statement list of a script or function. Instead use a variable initialized with a Function Expression to define a function within a block:

    if (x) {
        var foo = function() {};
    }

### Standards features

For maximum portability and compatibility, always prefer standards features over non-standards features (e.g., `string.charAt(3)` over `string[3]`).

### Wrapper objects for primitive types

There's no reason to use wrapper objects for primitive types, plus they're dangerous:

    var x = new Boolean(false);
    if (x) {
        alert("hi");  // Shows 'hi'.
    }

Don't do it!

However type casting is fine.

    var x = Boolean(0);
    if (x) {
        alert("hi");  // This will never be alerted.
    }
    typeof Boolean(0) === "boolean";
    typeof new Boolean(0) === "object";

This is very useful for casting things to number, string and boolean.

### delete

Prefer `this.foo = null`.

    Foo.prototype.dispose = function() {
        this.prop = null;
    };

Instead of:

    Foo.prototype.dispose = function() {
        delete this.prop;
    };

In modern JavaScript engines, changing the number of properties on an object is much slower than reassigning the values. The `delete` keyword should be avoided except when it is necessary to remove a property from an object's iterated list of keys, or to change the result of if (key in obj).

### eval()

`eval()` makes for confusing semantics and is dangerous to use if the string being eval()'d contains user input. There's usually a better, more clear, safer way to write your code, so its use is generally not permitted.

However `eval` makes deserialization considerably easier than the non-eval alternatives, so its use is acceptable for this task (for example, to evaluate RPC responses).

### with() {}

Using `with` clouds the semantics of your program. Because the object of the with can have properties that collide with local variables, it can drastically change the meaning of your program. For example, what does this do?

    with (foo) {
        var x = 3;
        return x;
    }

Answer: anything. The local variable `x` could be clobbered by a property of `foo` and perhaps it even has a setter, in which case assigning 3 could cause lots of other code to execute. Don't use `with`.

### this

The semantics of `this` can be tricky. At times it refers to

* the global object (in most places)
* the scope of the caller (in `eval`)
* a node in the DOM tree (when attached using an event handler HTML attribute)
* a newly created object (in a constructor)
* some other object (if function was call()ed or apply()ed).

Because this is so easy to get wrong, limit its use to those places where it is required:

* in constructors
* in methods of objects (including in the creation of closures)

### for-in loop

`for-in` loops are often incorrectly used to loop over the elements in an Array. This is however very error prone because it does not loop from 0 to length - 1 but over all the present keys in the object and its prototype chain.

* Only use for iterating over keys in an object/map/hash.
* Always use normal `for` loops when using arrays.

### Associative Arrays

Never use Array as a map/hash/associative array.

### Multiline string literals

Do not do this:

    var myString = "A rather long string of English text, an error message \
                    actually that just keeps going and going -- an error \
                    message to make the Energizer bunny blush (right through \
                    those Schwarzenegger shades)! Where was I? Oh yes, \
                    you've got an error and all the extraneous whitespace is \
                    just gravy.  Have a nice day.";

The whitespace at the beginning of each line can't be safely stripped at compile time; whitespace after the slash will result in tricky errors; and while most script engines support this, it is not part of ECMAScript.

Use string concatenation instead:

    var myString = "A rather long string of English text, an error message " +
        "actually that just keeps going and going -- an error " +
        "message to make the Energizer bunny blush (right through " +
        "those Schwarzenegger shades)! Where was I? Oh yes, " +
        "you've got an error and all the extraneous whitespace is " +
        "just gravy.  Have a nice day.";


### Array and Object literals

Never use constructors

    var arr = new Array();  // bad
    var obj = new Object(); // bad

Single-line array and object initializers are allowed when they fit on a line:

    var arr = [1, 2, 3];  // No space after [ or before ].
    var obj = {a: 1, b: 2, c: 3};  // No space after { or before }.

### Modifying prototypes of builtin objects

Modifying builtins like `Object.prototype` and `Array.prototype` are strictly forbidden. Modifying other builtins like `Function.prototype` is less dangerous but still leads to hard to debug issues in production and should be avoided.

### Internet Explorer's Conditional Comments

Don't do this:

    var f = function () {
        /*@cc_on if (@_jscript) { return 2* @*/  3; /*@ } @*/
    };

Conditional Comments hinder automated tools as they can vary the JavaScript syntax tree at runtime.
