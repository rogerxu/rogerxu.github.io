---
layout: post
title: WebSocket
---

## Server-Sent Events

SSE connections can only push data to the browser. For example, online stock quotes, twitter updating timeline or feed.

SSE are sent over traditional HTTP. That means they do not require a special protocol or server implementation to get working. WebSockets require full-duplex connections and new WebSocket servers to handle the protocol.

[Using server-sent events](https://developer.mozilla.org/en-US/docs/Server-sent_events/Using_server-sent_events)

Advantages of SSE over WebSockets:

* Transported over simple HTTP instead of a custom protocol
* Can be poly-filled with javascript to "backport" SSE to browsers that do not support it yet.
* Built in support for re-connection and event-id
* Simpler protocol

Ideal use cases of SSE:

* Stock ticker streaming
* twitter feed updating
* Notifications to browser

## WebSocket

WebSockets connections can both send data to the browser and receive data from the browser. For example, a chat application.

Since everything that can be done with SSE can also be done with WebSockets, many more browsers support WebSocket better than SSE.

Advantages of WebSockets over SSE:

* Real time, two directional communication.
* Native suport in more browsers.


