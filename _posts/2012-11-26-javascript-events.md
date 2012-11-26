---
layout: post
title: JavaScript Events
---

## Listening to Events

    addEventListener(type, listener, useCapture)

## Event Ordering

* Netscape 4 - capturing, which triggers event listeners from the top-most ancestor to the element
* Internet Explorer - bubbling, which triggers event listeners from the element, propagating up through its ancestors
* W3C - support for both event models. Events are first captured until they reach the target element; then, they bubble up again.

## Canceling Events

## The Event Object

## Event Libraries

## Context Change

## Delegating Events

## Custom Events

## Custom Events and jQuery Plug-Ins

## Non-DOM Events

Publish/Subscribe
