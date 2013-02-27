---
layout: post
title: Google Chrome
---

# Chrome Developer Tools

## Console API

[Console API Reference](https://developers.google.com/chrome-developer-tools/docs/console-api)

* console.clear

### Timer

`console.time(label)`
`console.timeEnd(label)`


    console.time("Array initialize");
    var array= new Array(1000000);
    for (var i = array.length - 1; i >= 0; i--) {
        array[i] = new Object();
    };
    console.timeEnd("Array initialize");


console.timeStamp
