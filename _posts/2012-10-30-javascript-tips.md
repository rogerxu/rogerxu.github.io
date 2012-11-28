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


