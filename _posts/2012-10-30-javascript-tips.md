---
layout: post
title: JavaScript Tips:
---

# JavaScript Tips

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
