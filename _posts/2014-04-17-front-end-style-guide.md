---
layout: post
title: Front-end Style Guide
---

## Resources

* [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwldrn/idiomatic.js)
* [JavaScript Style Guides And Beautifiers](http://addyosmani.com/blog/javascript-style-guides-and-beautifiers/)
* [Front-end Code Standards & Best Practices](http://isobar-idev.github.io/code-standards/)
* [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
* [Your code sucks, let's fix it - PHP Master Series 2012](http://www.slideshare.net/rdohms/your-code-sucks-lets-fix-it-php-master-series-2012)

## Common

- **File encoding:** UTF-8 without BOM
- **Line ending:** Unix style (LF)
- **Line length:** 80
- Trim trailing whitespace
- File names should be all lowercase in order to avoid confusion on case-sensitive platforms.

    ```javascript
    // bad
    appConfig.json

    // good
    app-config.json
    ```

## HTML

- **Indentation:** Use soft tabs set to 4 spaces

## CSS

- **Indentation:** Use soft tabs set to 4 spaces


## JavaScript

### Indentation

- Use soft tabs set to 4 spaces

- Array indentation

    ```javascript
    var items = [
        {
            id: 1,
            name: "a"
        },
        {
            id: 2,
            name: "b"
        }
    ];
    ```

- Binary and Ternary Operators

    ```javascript
    // good
    var result = flag ?
        longButSimpleOperandB : longButSimpleOperandC;

    // good
    var result = result ?
            moreComplicatedB :
            moreComplicatedC;

- Use indentation when making long method chains.

    ```javascript
    // bad
    $("#items").find(".selected").highlight().end().find(".open").updateCount();

    // good
    $("#items")
        .find(".selected")
            .highlight()
            .end()
        .find(".open")
            .updateCount();

    // bad
    var leds = stage.selectAll(".led").data(data).enter().append("svg:svg").class("led", true)
        .attr("width",  (radius + margin) * 2).append("svg:g")
        .attr("transform", "translate(" + (radius + margin) + "," + (radius + margin) + ")")
        .call(tron.led);

    // good
    var leds = stage.selectAll(".led")
            .data(data)
        .enter().append("svg:svg")
            .class("led", true)
            .attr("width",  (radius + margin) * 2)
        .append("svg:g")
            .attr("transform", "translate(" + (radius + margin) + "," + (radius + margin) + ")")
            .call(tron.led);
    ```

### Quotes

- jQuery and UI5 use double quotes `""`. Just keep the same.
- Use double quotes `""` in JSON.


### `use strict`

- Always declare `"use strict";` at the top of the module.

    ```javascript
    (function(global) {
        "use strict";

        // ...stuff...
    })(this);
    ```

### Naming Conventions

- Avoid single letter names. Be descriptive with your naming.

    ```javascript
    // bad
    function q() {
        // ...stuff...
    }

    // good
    function query() {
        // ...stuff...
    }
    ```

- Common naming conventions

| Type                      | Example                       |
| ------------------------- | --------------------------- - |
| Variable                  | `var adminUser = "admin";`    |
| Function                  | `function sayHello() {}`      |
| Class / Constructor       | `var user = new User();`      |
| Enum                      | `var color = Colors.Red;`     |
| Method                    | `user.sayHello();`            |
| Constant                  | `var ONE_SECOND = 1 * 1000;`  |


### Whitespaces

- Place 1 space before the leading brace.

    ```javascript
    // bad
    function test(){
        console.log("test");
    }

    // good
    function test() {
        console.log("test");
    }

    // bad
    dog.set("attr",{
        age: "1 year",
        breed: "Bernese Mountain Dog"
    });

    // good
    dog.set("attr", {
        age: "1 year",
        breed: "Bernese Mountain Dog"
    });
    ```

- No space after `[` or before `]`

    ```javascript
    // bad
    var items = [ 1, 2, 3 ];

    // good
    var items = [1, 2, 3];
    ```

- No space before `:`

    ```javascript
    // bad
    var item = {
        id : 123,
        name : "abc"
    };

    // good
    var item = {
        id: 123,
        name: "abc"
    };
    ```

- No space for parenthesis `()`

    ```javascript
    // bad
    if ( condition ) {
        // ...stuff...
    }

    // good
    if (condition) {
        // ...stuff...
    }

    // bad
    var foo = function ( arg1, arg2 ) {
        // ...stuff...
    };

    // good
    var foo = function(arg1, arg2) {
        // ...stuff...
    };
    ```

- Set off operators with spaces.

    ```javascript
    // bad
    var x=y+5;

    // good
    var x = y + 5;
    ```

- Place an empty newline at the end of the file.

    ```javascript
    // bad
    (function(global) {
        // ...stuff...
    })(this);
    ```

    ```javascript
    // bad
    (function(global) {
        // ...stuff...
    })(this);

    ```

### Braces

- Use braces.

    ```javascript
    // bad
    if (test)
        return false;

    // bad
    if (test) return false;

    // good
    if (test) {
        return false;
    }

    // bad
    function() { return false; }

    // good
    function() {
        return false;
    }
    ```

- Opening braces go on the same line as the statement.

    ```javascript
    // bad
    if (test)
    {
        return false;
    }

    // good
    function() {
        return false;
    }
    ```

### Commas

- Leading commas: **No**

- Additional trailing comma: **No**

    ```javascript
    // bad
    var item = {
        id: 123,
        name: "abc",
    };

    // good
    var item = {
        id: 123,
        name: "abc"
    };
    ```

### Semicolons

- Always use semicolons.

    ```javascript
    // bad
    (function() {
        var name = "abc"
        return name
    })()

    // good
    (function() {
        var name = "abc";
        return name;
    })();
    ```

- Relying on implicit insertion can cause subtle, hard to debug problems. Don't do it. You're better than that.

    ```javascript
    // bad
    User.prototype.getAge = function() {
        return 42;
    } // => No semicolon here.

    (function() {
        console.log("hello");
    })(); // => Reports error
    ```

### Comments

- Use `/** .. */` for api comments.

- Use `//` for single line comments. Put an empty line before the comment.

- Use `// FIXME:` to annotate problems.

- Use `// TODO:` to annotate solutions to problems.


### Variables

- Always use `var` to declare variables. We should avoid polluting the global namespace.

    ```javascript
    // bad
    item = new Item();

    // good
    var item = new Item();
    ```

- Declare one variable per `var` statement, it makes it easier to re-order the lines. Ignore Crockford on this, and put those declarations wherever they make sense.

    ```javascript
    // bad
    var items = getItems(),
        flag = true,
        name = "abc";

    // good
    var items = getItems();
    var flag = true;
    var name = "abc";
    ```

- Never use the `const` keyword as it not supported in Internet Explorer.


### `||` and `&&`

- Use `||` to assign default value

    ```javascript
    // bad
    var name = event.getParameter("name") ? event.getParameter("name") : "";
    var count = event.getParameter("count") ? event.getParameter("count") : 10;

    // good
    var name = event.getParameter("name") || "";
    var count = event.getParameter("count") || 10;
    ```

### `==` and `===`

JavaScript data type equality table:

| Type                      | True/False                    |
| ------------------------- | ----------------------------- |
| `undefined`               | `false`                       |
| `null`                    | `false`                       |
| `0`                       | `false`                       |
| `NaN`                     | `false`                       |
| `1`                       | `true`                        |
| `""`                      | `false`                       |
| `"abc"`                   | `true`                        |
| `Object`                  | `true`                        |


- Use `===` and `!==` over `==` and `!=`

    ```javascript
    // bad
    if (num == 1) {
        // ...stuff...
    }

    // good
    if (num === 1) {
        // ...stuff...
    }
    ```

- Use shortcuts.

    ```javascript
    // bad
    if (str !== "") {
        // ...stuff...
    }

    // good
    if (str) {
        // ...stuff...
    }

    // bad
    if (str === "") {
        // ...stuff...
    }

    // good
    if (!str) {
        // ...stuff...
    }

    // bad
    if (obj === null || obj === undefined) {
        // ...stuff...
    }

    // good
    if (obj == null) {
        // ...stuff...
    }

    // bad
    if (array.length > 0) {
        // ...stuff...
    }

    // good
    if (array.length) {
        // ...stuff...
    }

    // bad
    if (array.length === 0) {
        // ...stuff...
    }

    // good
    if (!array.length) {
        // ...stuff...
    }
    ```

### Types

- String

    ```javascript
    typeof value === "string"
    ```

- Number

    ```javascript
    typeof value === "number"
    ```

- Boolean

    ```javascript
    typeof value === "boolean"
    ```

- Object

    ```javascript
    typeof value === "object"
    ```

- Array

    ```javascript
    Array.isArray(value)
    ```

- `null`

    ```javascript
    value === null
    ```

- `undefined`

    ```javascript
    typeof value === "undefined"
    ```

- `null` or `undefined`

    ```javascript
    value == null
    ```

- Check property

    ```javascript
    obj.hasOwnProperty("price")
    "price" in object
    ```

### Coercion

- Convert to String

    ```javascript
    var num = 10;

    // bad
    var str = num + "";

    // good
    var str = "" + num;

    // bad
    var str = "" + num + " items";

    // good
    var str = num + " items";
    ```

- Convert to Number

    ```javascript
    var str = '9';

    // bad
    var num = new Number(str);

    // bad
    var num = +str;

    // bad
    var num = str >> 0;

    // bad
    var num =  parseInt(str);

    // good
    var num = Number(str);

    // good
    var num =  parseInt(str, 10);
    ```

- Convert to Boolean

    ```javascript
    var flag = 0;

    // bad
    var isShow = new Boolean(flag);

    // good
    var isShow = Boolean(flag);

    // good
    var isShow =  !!flag;
    ```


### Strings

- Strings longer than 80 characters should be written across multiple lines using string concatenation.

    ```javascript
    // bad
    var errorMessage = "This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.";

    // bad
    var errorMessage = "This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.";

    // good
    var errorMessage = "This is a super long error that was thrown because " +
        "of Batman. When you stop to think about how Batman had anything to do " +
        "with this, you would get nowhere fast.";
    ```

- Use `Array#join` instead of string concatenation when programmatically building up a string.

    ```javascript
    var messages = ["message 1", "message 2"];

    // bad
    function show(messages) {
        var str = "";

        var i;
        for (i = 0; i < length; i++) {
            str += messages[i] + "|";
        }

        return str;
    }

    // good
    function show(messages) {
        var str = messages.join("|");
        return str;
    }
    ```


### Objects

- Use the literal syntax for object creation

    ```javascript
    // bad
    var item = new Object();

    // good
    var item = {};
    ```

- Don't use reserved words as keys. It won't work in IE8.

    ```javascript
    // bad
    var item = {
        default: {
            name: "abc"
        },
        private: true
    };

    // good
    var item = {
        defaults: {
            name: "abc"
        },
        hidden: true
    };
    ```

- Use readable synonyms in place of reserved words.

    ```javascript
    // bad
    var item = {
        class: "admin"
    };

    // bad
    var item = {
        klass: "admin"
    };

    // good
    var item = {
        type: "admin"
    };
    ```


### Properties

- Use dot notation when accessing properties.

    ```javascript
    var item = {
        id: 1234,
        name: "abc"
    };

    // bad
    var name = item["name"];

    // good
    var name = item.name;
    ```

- Use subscript notation `[]` when accessing properties with a variable.

    ```javascript
    var item = {
        id: 1234,
        name: "abc"
    };

    function getProp(key) {
        return item[key];
    }

    var name = getProp("name");
    ```


### Arrays

- Use the literal syntax for array creation

    ```javascript
    // bad
    var items = new Array();

    // good
    var items = [];
    ```

- Use `Array#push` to add an item.

    ```javascript
    var items = [];

    // bad
    items[items.length] = "abc";

    // good
    items.push("abc");
    ```

- Use `Array#slice` to copy an array.

    ```javascript
    var items = [1, 2, 3];
    var n = items.length;
    var itemsCopy = [],

    // bad
    var i;
    for (i = 0; i < n; i++) {
        itemsCopy[i] = items[i];
    }

    // good
    itemsCopy = items.slice();
    ```

- Use `Array#slice` to convert an array-like object to an array.

    ```javascript
    function trigger() {
        var args = Array.prototype.slice.call(arguments);
    }
    ```


### `for in` loop

`for in` loops are often incorrectly used to loop over the elements in an Array. This is however very error prone because it does not loop from `0` to `length - 1` but over all the present keys in the object and its prototype chain.

- Only use `for in` with `hasOwnProperty` for iterating over keys in an object/map/hash.

    ```javascript
    var key;
    for (key in obj) {
        if (obj.hasOwnProperty(key)) {
            console.log(key, obj[key]);
        }
    }
    ```

- Use normal `for` loops when using arrays.

    ```javascript
    var i;
    for (i = 0; i < items.length; i++) {
        console.log(i, items[i]);
    }
    ```

- Use utility helper like `Underscore` to do iteration.

    ```javascript
    // array
    util.each(items, function(item, index) {
        console.log(index, item);
    });

    // object
    util.each(obj, function(value, key) {
        console.log(key, value);
    });
    ```

### Functions

- Function expressions

    ```javascript
    // anonymous function expression
    var anonymous = function() {
        return true;
    };

    // named function expression
    var named = function named() {
        return true;
    };

    // immediately-invoked function expression (IIFE)
    (function() {
        console.log("Hello World!");
    })();
    ```

- Never declare a funciton in a non-function block (`if`, `while`, etc). Assign the function to a variable instead.

    ```javascript
    // bad
    if (currentUser) {
        function test() {
            console.log("Nope.");
        }
    }

    // good
    var test;
    if (currentUser) {
        test = function() {
            console.log("Yup.");
        };
    }
    ```

### Prototypes

- Don't modify prototypes of built-in objects.

    Modifying built-in objects like `Object.prototype` and `Array.prototype` are strictly forbidden. Modifying other builtins like `Function.prototype` is less dangerous but still leads to hard to debug issues in production and should be avoided.

- Assign methods to the prototype object, instead of overwriting the prototype with a new object. Overwriting the prototype makes inheritance impossible: by resetting the prototype you'll overwrite the base.

    ```javascript
    function User() {
        console.log("new user");
    }

    // bad
    User.prototype = {
        login: function() {
            console.log("login");
        },

        logout: function() {
            console.log("logout");
        }
    };

    // good
    User.prototype.login = function() {
        console.log("login");
    };

    User.prototype.logout = function() {
        console.log("logout");
    };
    ```

- Methods can return `this` to help with method chaining.

    ```javascript
    // bad
    Jedi.prototype.jump = function() {
        this.jumping = true;
        return true;
    };

    Jedi.prototype.setHeight = function(height) {
        this.height = height;
    };

    var luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20); // => undefined

    // good
    Jedi.prototype.jump = function() {
        this.jumping = true;
        return this;
    };

    Jedi.prototype.setHeight = function(height) {
        this.height = height;
        return this;
    };

    var luke = new Jedi();

    luke.jump()
        .setHeight(20);
    ```

- It's okay to write a custom `toString()` method, just make sure it works successfully and causes no side effects.

    ```javascript
    function Jedi(options) {
        options || (options = {});
        this.name = options.name || "no name";
    }

    Jedi.prototype.getName = function() {
        return this.name;
    };

    Jedi.prototype.toString = function() {
        return "Jedi - " + this.getName();
    };
    ```

### `this`

The semantics of `this` can be tricky. At times it refers to

- the global object (in most places)
- the scope of the caller (in `eval()`)
- a node in the DOM tree (when attached using an event handler HTML attribute)
- a newly created object (in a constructor)
- some other object (if function invokes `call()` or `apply()`).

`this` is so easy to get wrong, limit its use to

- in constructors

    ```javascript
    function User(name) {
        this.name = name;
    }

    User.prototype.greet = function() {
        return this.name;
    };

    var user = new User("abc");
    user.greet();
    ```
- in methods of objects (including in the creation of closures)

    ```javascript
    var obj = {
        name: "abc",
        greet: function() {
            console.log(this.name);
        }
    };

    obj.greet();
    ```

- Use alias for `this` as the scope object.

    ```javascript
    obj.loadItems = function() {
        var self = this;

        util.getJSON("/items", function(data) {
            self.items = data.results;
        });
    };
    ```

### `eval()`

- Don't use `eval()`.

    `eval()` makes for confusing semantics and is dangerous to use if the string being eval()'d contains user input. There's usually a better, more clear, safer way to write your code, so its use is generally not permitted.

### `with`

- Don't use `with`.

    Using `with` clouds the semantics of your program. Because the object of the with can have properties that collide with local variables, it can drastically change the meaning of your program.

    For example, what does this do?

    ```javascript
    with (foo) {
        var x = 3;
        return x;
    }
    ```

    *Answer:* anything. The local variable `x` could be clobbered by a property of `foo` and perhaps it even has a setter, in which case assigning 3 could cause lots of other code to execute.

