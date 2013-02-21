---
layout: post
title: JavaScript Tips
---

## Useful Code Snippets

### Initialization

Use function block to avoid global variables.

    (function(window, document, $, undefined) {
        // insert code here
    })(this, document, jQuery);

### Replacement for setInterval()

    (function loops() {
        doStuff();

        $("#update").load("abc.php", function() {
            loops();
        });

        setTimeout(loops, 100);
    })();


## Array

### Array.reduce

Apply a function against an accumulator and each value of the array (from left to right) as to reduce it to a single value.

Syntax: `array.reduce(callback[, initialValue])`

Example:

    var result = [1, 2, 3, 4].reduce(function(previousValue, currentValue, index, array) {
        return previousValue + currentValue;
    });
    console.log(result); // 10

### jQuery.merge

    var arr1 = [1, 2, 3];
    jQuery.merge(arr1, [4, 5]);
    console.log(arr1); // [1, 2, 3, 4, 5]

### jQuery.makeArray

    jQuery.makeArray("a"); // ["a"]
    jQuery.makeArray(["a"]); // ["a"]

