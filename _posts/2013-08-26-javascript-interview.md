---
layout: post
title: JavaScript Interview
---

## Resources

* [Free Javascript Test](http://www.mytestpapers.com/javascript-test/)
* [JavaScript Exam](http://www.wepapers.com/Papers/19632/JavaScript_Exam)
* [Exam 2 Sample Test Questions](http://www.willamette.edu/~gorr/classes/cs130/Labs/myQuest2.html)

## Questions

### Types

    Object.prototype.toString.call([])          // "[object Array]"
    Object.prototype.toString.call({})          // "[object Object]"
    Object.prototype.toString.call(2)           // "[object Number]"
    Object.prototype.toString.call(null)        // "[object Null]"
    Object.prototype.toString.call(undefined)   // "[object Undefined]"

### Array

    [1, 2, 3]; // Result: [1, 2, 3]
    new Array(1, 2, 3); // Result: [1, 2, 3]

    [3]; // Result: [3]
    new Array(3); // Result: []
    new Array('3') // Result: ['3']
    new Array(3, 4, 5); // Result: [3, 4, 5]

### Deleting Properties

Question: How to delete the `foo` property in `obj`?

    var obj = {
        foo: "foo",
        bar: "bar"
    };

Answer:

    delete obj.foo;


Question: How to delete the `foo` element in `array`?

    var array = ["hello", "world", "foo", "bar"];

Answer:

    var index = array.indexOf("foo");
    array.splice(index, 1); // remove 3

Question: How to remove every `bar` element in `array`?

    var array = ["foo", "bar", "bar", "foo", "bar"];

Answer:

    for (var i = array.length - 1; i >= 0; i--) {
        if (array[i] === "bar") {
            array.splice(i, 1);
        }
    }

### for-in loop

    for (var i in foo) {
        if (foo.hasOwnProperty(i)) {
            console.log(i);
        }
    }

### `arguments`

Question: How to pass `arguments`?

    function foo() {
        bar.apply(null, arguments);
    }

    function bar(a, b, c) {
        // do stuff here
    }

### Automatic Semicolon Insertion

Question: What is the output of the following code?

    function MyClass() {
    }

    MyClass.prototype.myMethod = function() {
        return 42;
    }

    (function() {
        var obj = new MyClass();
        var result = obj.myMethod();
        console.log(result);
    })();


Answer: JavaScript error due to missing a semicolon at the end of `myMethod` function.

JavaScript error - the function returning 42 is called with the second function as a parameter, then the number 42 is "called" resulting in an error.

    function MyClass() {
    }

    MyClass.prototype.myMethod = function() {
        return 42;
    }(function() {
        var obj = new MyClass();
        var result = obj.myMethod();
        console.log(result);
    })();

### Hoisting

Question: What happens in the following code?

    bar();
    var bar = function() {};
    var someValue = 42;

    test();
    function test(data) {
        if (false) {
            goo = 1;

        } else {
            var goo = 2;
        }
        for(var i = 0; i < 100; i++) {
            var e = data[i];
        }
    }

Answer:

    // var statements got moved here
    var bar, someValue; // default to 'undefined'

    // the function declaration got moved up too
    function test(data) {
        var goo, i, e; // missing block scope moves these here
        if (false) {
            goo = 1;

        } else {
            goo = 2;
        }
        for (i = 0; i < 100; i++) {
            e = data[i];
        }
    }

    bar(); // fails with a TypeError since bar is still 'undefined'
    someValue = 42; // assignments are not affected by hoisting
    bar = function() {};

    test();


### Inheritance

#### prototype

    function Foo() {
        this.value = 42;
    }

    Foo.prototype = {
        method: function() {}
    };

    function Bar() {
    }

    // Set Bar's prototype to a new instance of Foo
    Bar.prototype = new Foo();
    Bar.prototype.foo = "Hello World";

    // Make sure to list Bar as the actual constructor
    Bar.prototype.constructor = Bar;

    var test = new Bar(); // create a new bar instance

    // The resulting prototype chain
    test [instance of Bar]
        Bar.prototype [instance of Foo]
            { foo: 'Hello World' }
            Foo.prototype
                { method: ... }
                Object.prototype
                    { toString: ... /* etc. */ }

It is important to note that new Bar() does not create a new Foo instance, but reuses the one assigned to its prototype; thus, all Bar instances will share the same value property.

#### Factories

    function Foo() {
        var obj = {};
        obj.value = "blub";

        var private = 2;

        obj.someMethod = function(value) {
            this.value = value;
        };

        obj.getPrivate = function() {
            return private;
        };

        return obj;
    }

Downsides:

1. It uses more memory since the created objects do not share the methods on a prototype.
2. In order to inherit, the factory needs to copy all the methods from another object or put that object on the prototype of the new object.


### Date, Time Zone

Question: Please implement the `formatDateTimeZone` function.

    /**
     * Formats the Date object in the specified time zone.
     *
     * @param {Date} date - The Date object to be formattted.
     * @param {Integer} timezone - Time zone in hours. 9 means +9:00, -9 means -9:00.
     * @return The date time string with the specified time zone in the ISO8601 format like "2013-08-18T09:12:00.789+09:00".
     */
    function formatDateTimeZone(date, timezone) {
        // Implement the function here
    }

    var date = new Date();
    var dateStr = formatDateTimeZone(date, 9);

Reference:

Constructor for `Date` class:

    Date(milliseconds)

Methods in `Date` instance:

    getDate(),          setDate(),          getUTCDate(),           setUTCDate(),
    getDay(),                               getUTCDay(),
    getFullYear(),      setFullYear(),      getUTCFullYear(),       setUTCFullYear(),
    getHours(),         setHours(),         getUTCHours(),          setUTCHours(),
    getMilliseconds(),  setMilliseconds(),  getUTCMilliseconds(),   setUTCMilliseconds(),
    getMinutes(),       setMinutes(),       getUTCMinutes(),        setUTCMinutes(),
    getMonth(),         setMonth(),         getUTCMonth(),          setUTCMonth(),
    getSeconds(),       setSeconds(),       getUTCSeconds(),        setUTCSeconds(),
    getTime(),          setTime(),
    getTimezoneOffset(),
    getYear(),          setYear(),
    toString(),         toUTCString(),      toLocaleString()


Answer:

Solution 1: Use local time

    function formatDateTimeZone(date, timezone) {
        var localTime = date.getTime();
        var localOffset = 1000 * 60 * date.getTimezoneOffset();
        var utcTime = localTime + localOffset;

        var destOffset = 1000 * 60 * 60 * timezone;
        var destTime = utcTime + destOffset;
        var destDate = new Date(destTime);
        console.log(destDate.toLocaleString());

        var _year = destDate.getFullYear();
        var _month = destDate.getMonth();
        var _date = destDate.getDate();
        var _hours = destDate.getHours();
        var _minutes = destDate.getMinutes();
        var _seconds = destDate.getSeconds();
        var _milliseconds = destDate.getMilliseconds();

        var str = formatISO8601(_year, _month + 1, _date, _hours, _minutes, _seconds, _milliseconds, timezone);

        return str;
    }

Solution 2: Use UTC time

    function formatDateTimeZone(date, timezone) {
        var localTime = date.getTime();
        var destOffset = 1000 * 60 * 60 * timezone;
        var destUTCTime = localTime + destOffset;
        var destUTCDate = new Date(destUTCTime);
        console.log(destUTCDate.toUTCString());

        var _year = destUTCDate.getUTCFullYear();
        var _month = destUTCDate.getUTCMonth();
        var _date = destUTCDate.getUTCDate();
        var _hours = destUTCDate.getUTCHours();
        var _minutes = destUTCDate.getUTCMinutes();
        var _seconds = destUTCDate.getUTCSeconds();
        var _milliseconds = destUTCDate.getUTCMilliseconds();

        var str = formatISO8601(_year, _month + 1, _date, _hours, _minutes, _seconds, _milliseconds, timezone);

        return str;
    }

ISO8601 Date Format

    function formatISO8601(year, month, date, hours, minutes, seconds, milliseconds, timezoneOffsetInHours) {
        var dateSeg = year + "-" + month + "-" + date; // yyyy-MM-dd
        var timeSeg = hours + ":" + minutes + ":" + seconds + "." + milliseconds; // hh:mm:ss.SSS

        var timezoneSeg = "";
        if (timezoneOffsetInHours === 0) {
            timezoneSeg = "Z"
        } else {
            if (timezoneOffsetInHours > 0) {
                timezoneSeg = "+";
            }

            timezoneSeg += timezoneOffsetInHours + ":00";
        }

        var str = dateSeg + "T" + timeSeg + timezoneSeg;

        return str;
    }


### MVC

MainView.xml

    <ui:View controller="MainView.controller.js">

        <Text id="output" text="N/A"><Text>

        <!-- Include SubView -->
        <ui:View id="subView" path="SubView.xml"></ui:View>

    </ui:View>


MainView.controller.js

    {
        onInit: function() {
            console.log("MainView.onInit");

            // press the button
            var button = this.byId("subView").byId("button");
            button.firePress();
        },

        showMessage: function(msg) {
            this.byId("output").setText(msg);
        }
    };

SubView.xml

    <ui:View controller="SubView.controller.js">

        <FancyButton id="button" press="getMessage"></FancyButton>

    </ui:View>


SubView.controller.js

    {
        onInit: function() {
            console.log("SubView.onInit");
        },

        getMessage: function(event) {
            // mockup server request
            setTimeout(function() {
                var message = "Hello World!";
                console.log(message);

                // TODO: try to invoke MainView.showMessage()
            }, 1000);
        }
    };

Console log:

    "SubView.onInit"
    "MainView.onInit"
    "Hello World!"
