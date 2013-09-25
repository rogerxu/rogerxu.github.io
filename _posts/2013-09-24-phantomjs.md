---
layout: post
title: PhantomJS
---

## Introduction

PhantomJS - Scriptable Headless WebKit

Documentation: <http://phantomjs.org/>

## Installation

* [Download and Installation](http://phantomjs.org/download.html)

### Windows

Download `phantomjs-1.9.2-windows.zip` (6.8 MB) and extract (unzip) the content.

The executable `phantomjs.exe` is ready to use.


### Mac OS X

    TODO

### Linux

    $ tar -xvjf phantomjs-1.9.2-linux-x86_64.tar.bz2
    $ sudo ln -s /usr/local/share/phantomjs-1.9.2-linux-x86_64/ /usr/local/share/phantomjs
    $ sudo ln -s /usr/local/share/phantomjs/bin/phantomjs /usr/local/bin/phantomjs
    $ whereis phantomjs
    $ phantomjs --version


### Source Code

    TODO


## Usage

    $ phantomjs hello.js

## Features

### Headless Testing

    $ phantomjs runner.js http://localhost:8080/web/test.qunit.html

### Screen Capture

    page.render();


