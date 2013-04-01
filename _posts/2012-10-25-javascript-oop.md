---
layout: post
title: JavaScript Object-oriented Programming
---

# JavaScript Object-oriented Programming

## Concept

### JavaScript Object Layout

[JavaScript diagrams](http://www.mollypages.org/misc/index.mp)

[JavaScript Object Layout](http://www.mollypages.org/misc/js.mp)

![JavaScript Object Layout](http://www.mollypages.org/misc/jsobj.jpg)


    // Constructor
    function Foo(name) {
        this.name = name;
    }

#### `__proto__`

    var f1 = new Foo("f1");
    f1.__proto__ -> Foo.prototype
    Foo.prototype.__proto__ -> Object.prototype
    Object.prototype.__proto__ -> null

    Foo.prototype.intro = function() {
        alert(this.name);
    };
    f1.intro();

    Foo.greet = function() {
        alert("Hello!");
    };
    Foo.greet();

### Scope

    function foo() {
        var x = 1;

        if (true) {
            var x = 2;
        }

        alert(x); // 2
    }

### Hoisting

    function foo() {
        var x = 1;
        alert(y); // undefined

        if (true) {
            var y = 2;
        }
    }

JavaScript interprets the function as following:

    function foo() {
        var x;
        var y;

        x = 1;
        alert(y);

        if (true) {
            y = 2;
        }
    }

### Activation Object / Variable Object

    funciton Outer() {
        var a = 0;
        var Inner = function() {
            a++;
            alert("foo");
        };

        return Inner;
    }

    var inner = Outer();
    inner();

### Constructor

Create a rabbit with new keyword

    function Rabbit(name) {
        this.name = name;
        this.speak = function(line) {};
    }

    var killerRabbit = new Rabbit("killer");
    console.log(killerRabbit.constructor); // Rabbit

Create a rabbit instance without new keyword

    function makeRabbit(name) {
        return {
            name: name,
            speak: function(line) {}
        }
    }

    var blackRabbit = makeRabbit("black");
    console.log(blackRabbit.constructor); // Object

### instanceof

    var result = object instanceof Constructor;

    Object.prototype.hasPrototype = function(prototype) {
        function DummyConstructor() {}
        DummyConstructor.prototype = prototype;
        return this instanceof DummyConstructor;
    };

    console.log(javascript.hasPrototype(Item)); // true

### Prototype

    function Item(name) {
        this.name = name;
        this.category = "web technology";
    }

    var itemA = new Item("html");
    var itemB = new Item("javascript");

If we change the category property of either one object, it will not affect others.

    itemB.category = "programming language";
    console.log(itemA.category); // "web technology"

Sometimes we want to share properties/functions for objects with same constructor. So we can use `prototype` object.

    function Item(name) {
        this.name = name;
    }

    Item.prototype.category = "web technology";

### hasOwnProperty

    function forEachIn(object, action) {
        for (var property in object) {
            if (Object.property.hasOwnProperty.call(object, property)) {
                action(property, object[property]);
            }
        }
    }

#### Dictionary


## Inheritance

### Inherit Constructor

Inherit DetailedItem from Item constructor.

    function Item() {
        this.category = "programming";
    }

    function DetailedItem(name, description) {
        this.name = name;
        this.description = description;
    }

    DetailedItem.prototype = new Item();
    DetailedItem.prototype.constructor = DetailedItem;

    var javascript = new DetailedItem("JavaScript", ".js files");
    console.log(javascript.category);

We can also inherit DetailedItem from Item prototype object.

    function Item() {}
    Item.prototype.category = "programming";

    function DetailedItem(name, description) {
        this.name = name;
        this.description = description;
    }

    DetailedItem.prototype = Item.prototype;
    DetailedItem.prototype.constructor = DetailedItem;

    var javascript = new DetailedItem("JavaScript", ".js files");
    console.log(javascript.category); // "programming"

But there is a problem. If we change DetailedItem prototype, it will also change Item prototype. Because they are the same object now.

    console.log(Item.prototype.constructor); "DetailedItem"

So we can fix this problem with a broker empty object.

    function Item() {}
    Item.prototype.category = "programming";

    function F() {}
    F.prototype = Item.prototype;

    function DetailedItem(name, description) {
        this.name = name;
        this.description = description;
    }

    DetailedItem.prototype = new F();
    DetailedItem.prototype.constructor = DetailedItem;

    var javascript = new DetailedItem("JavaScript", ".js files");
    console.log(javascript.category); "programming"

    console.log(Item.prototype.constructor); "Item"

So we can write a common function:

    function extend(Child, Parent) {
        function F() {}
        F.prototype = Parent.prototype;
        Child.prototype = new F();
        Child.prototype.constructor = Child;
        Child.super = Parent.prototype;
    }

### Inherit Object
    var Item = {
        category: "programming"
    };

    var DetailedItem = {
        name: "javascript"
    };

We can write a clone function.

    function clone(object) {
        function OneShotConstructor() {}
        OneShotConstructor.prototype = object;
        return new OneShotConstructor();
    }

    var DetailedItem = clone(Item);
    DetailedItem.name = "javascript";

    console.log(DetailedItem.category); // "programming"

### OOP without Constructor

The prototype itself is the most important aspect of an object type, and the constructor is just an extension of that, a special kind of method.

    Object.prototype.create = function() {
        var object = clone(this);

        // construct is a user defined constructor function
        if (typeof object.construct == "function") {
            object.construct.apply(object, arguments);
        }

        return object;
    };

    Object.prototype.extend = function(properties) {
        var result = clone(this);
        forEachIn(properties, function(name, value) {
            result[name] = value;
        });

        return result;
    };

    Object.prototype.hasPrototype = function(prototype) {
        function DummyConstructor() {}
        DummyConstructor.prototype = prototype;
        return this instanceof DummyConstructor;
    };

    var Item = {
        construct: function(name) {
            this.name = name;
        },
        inspect: function() {
            console.log("it is", this.name, ".");
        }
    };

    var DetailedItem = Item.extend({
        construct: function(name, details) {
            Item.construct.call(this, name);
            this.details = details;
        },
        inspect: function() {
            console.log("you see", this.name, ",", this.details, ".");
        }
    });

    var detailedItem1 = DetailedItem.create("item 1", "it is detailed item 1");
    detailedItem1.inspect();
    console.log(detailedItem1.hasPrototype(Item));

## Modularity

### require

    var dependencies = {
        "ObjectTools.js": ["FunctionalTools.js"],
        "Dictionary.js": ["ObjectTools.js"],
        "TestModule.js": ["FunctionalTools.js", "Dictionary.js"]
    };

    function require(file) {
        if (dependencies[file]) {
            var files = dependencies[file];
            for (var i = 0; i < files.length; i++) {
                require(files[i]);
            }
        }

        if (!loadedFiles[file]) {
            loadedFiles[file] = true;
            load(file);
        }
    }

### provide

    function provide(values) {
        forEachIn(values, function(name, value) {
            window[name] = value;
        });
    }

    (function() {
        var names = ["A", "B", "C"];

        provide({
            getName: function(number) {
                return names[number];
            }
        });
    })();

## Resources
* [JavaScript继承机制的设计思想](http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)
* [JavaScript面向对象编程（二）：构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html)
* [JavaScript面向对象编程（三）：非构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html)
* [Eloquent JavaScript: Object-oriented Programming](http://eloquentjavascript.net/chapter8.html#p2d3cad23)

