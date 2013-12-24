---
layout: post
title: AngularJS
---

## Introduction

AngularJS: <http://angularjs.org/>

AngularJS is a structural framework for dynamic web apps.

## Installation

Maven

    <dependency>
    </dependency>


## Controllers

## Filters

## Templates

## Services

## Dependency Injection

Dependency Injection (DI) is a software design pattern that deals with how code gets hold of its dependencies.

## Providers

value

    var app = angular.module('app', []);
    app.value('clientId', 'a12345654321x');

    app.controller('DemoController', ['clientId', function DemoController(clientId) {
        tis.clientId = clientId;
    }]);


factory

    app.factory('clientId', function clientIdFactory() {
        return 'a12345654321x';
    });

    app.factory('apiToken', ['clientId', function apiTokenFactory(clientId) {
        var encrypt = function(data1, data2) {
            // NSA-proof encryption algorithm:
            return (data1 + ':' + data2).toUpperCase();
        };

        var secret = window.localStorage.getItem('myApp.secret');
        var apiToken = encrypt(clientId, secret);

        return apiToken;
    }]);

service

    function UnicornLauncher(apiToken) {

        this.launchedCount = 0;
        this.launch() {
            // make a request to the remote api and include the apiToken
            ...
            this.launchedCount++;
        }
    }

    app.factory('unicornLauncher', ['apiToken', function(apiToken) {
        return new UnicornLauncher(apiToken);
    }]);

    app.service('unicornLauncher', ['apiToken', UnicornLauncher]);

provider

    app.provider('unicornLauncher', function UnicornLauncherProvider() {
        var useTinfoilShielding = false;

        this.useTinfoilShielding = function(value) {
            useTinfoilShielding = !!value;
        };

        this.$get = ["apiToken", function unicornLauncherFactory(apiToken) {

            // let's assume that the UnicornLauncher constructor was also changed to
            // accept and use the useTinfoilShielding argument
            return new UnicornLauncher(apiToken, useTinfoilShielding);
        }];
    });

    app.config(['unicornLauncherProvider', function(unicornLauncherProvider) {
        unicornLauncherProvider.useTinfoilShielding(true);
    }]);

constant

Since the config function runs in the configuration phase when no services are available, it doesn't have access even to simple value objects created via Value recipe.

    app.constant('planetName', 'Greasy Giant');

    app.config(['unicornLauncherProvider', 'planetName', function(unicornLauncherProvider, planetName) {
        unicornLauncherProvider.useTinfoilShielding(true);
        unicornLauncherProvider.stampText(planetName);
    }]);

    app.controller('DemoController', ['clientId', 'planetName', function DemoController(clientId, planetName) {
        this.clientId = clientId;
        this.planetName = planetName;
    }]);


## Configuration

## ngResource

## Routing
