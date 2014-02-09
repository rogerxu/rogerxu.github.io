---
layout: post
title: AngularJS
---

## Introduction

AngularJS: <http://angularjs.org/>

AngularJS is a structural framework for dynamic web apps.

## Installation

### Maven

    <dependency>
        <groupId>org.webjars</groupId>
        <artifactId>angularjs</artifactId>
        <version>1.2.10</version>
    </dependency>

### Yeoman

    $ npm install -g generator-angular
    $ yo angular

### Bower

    $ bower install angular --save


## Advantages

### 1. MVC done right

Most frameworks implement MVC by asking you to split your app into MVC components, then require you to write code to string them up together again. That's a lot of work.

### 2. A declarative user interface

Angular uses HTML to define the app's user interface.

### 3. Data models are POJO

Data models in Angular are plain old JavaScript objects (POJO) and don't require extraneous getter and setter functions.

Traditional data models are gatekeepers of data and are responsible for data persistence and server syncing. Those data models behave like smart data providers.

Angular's data models behave more like a cork board. A cork board is nothing more than a temporary storage area for people to put and retrieve data. Angular quietly watches for changes to these properties and updates the view automatically.

### 4. Behavior with directives

As a rule of thumb, your controller should not manipulate the DOM directly. All DOM manipulations should be performed by directives.

### 5. Flexibility with filters

Filters are designed to be standalone functions that are separate from your app, and are only concerned with data transformations.

### 6. Write less code

* The view is defined using HTML, which is more concise.
* Data models are simpler to write without getters/setters.
* Data-binding
* Directives are separate from app code.
* Filters allow you to manipulate data on the view level without changing the controllers.

### 7. DOM manipulations where they belong

With Angular, DOM manipulation code should be inside directives and not in the view.

### 8. Service providers where they belong

Controllers in Angular are simple functions that have one job only, which is to manipulate the scope. Unlike other frameworks, controllers are not objects and don't inherit from anything.

### 9. Context aware communication

A PubSub system is a pretty common tool that allows for decoupled communication.

The PubSub system in Angular `broadcast()` will send a message to all children controllers, while `emit()` will send a message to all ancestors.

The scopes inherit the properties of their parent scopes.

### 10. Unit testing ready

Angular's unit tests are able to usurp DI to perform unit testing by injecting mock data into your controller and measuring the output and behavior.

Angular already has a mock HTTP provider to inject fake server responses into controllers.


## Controllers

## Filters

## Templates

## Services

## Data Binding

* `ngBind`

The `ngBind` attribute tells Angular to replace the text content of the specified HTML element with the value of a given expression.

Typically, you don't use `ngBind` directly, but instead you use the double curly markup like \{\{expression\}\} which is similar but less verbose.

It is preferable to use `ngBind` instead of \{\{expression\}\} when a template is momentarily displayed by the browser in its raw state before Angular compiles it.

    <p ng-bind="name"></p>

* `ngCloak`

The `ngClock` directive is used to prevent the Angular html template from being briefly displayed by the browser in its raw form while your application is loading. Use this directive to avoid the undesirable flicker effect caused by the html template display. Flash of unstyled content (FOUC).

For the best result, the `angular.js` script must be loaded in the head section of the html document.

    <p ng-cloak>{{name}}</p>

Add the following css rule in the external stylesheet of the application.

    [ng\:cloak], [ng-cloak], [data-ng-cloak], [x-ng-cloak], .ng-cloak, .x-ng-cloak {
        display: none !important;
    }


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

Application routes in Angular are declared via the `$routeProvider`, which is the provider of the `$route` service. Using this feature we can implement deep linking, which lets us utilize the bowser's history (back and forward navigation) and bookmarks.


    // Configuring $routeProvider
    app.config(['$routeProvider', function($routeProvider) {
        $routeProvider
            .when('/', {
                templateUrl: 'views/main.html',
                controller: 'MainCtrl'
            })
            .when('/orders', {
                templateUrl: 'views/show_orders.html',
                controller: 'ShowOrdersCtrl'
            })
            .when('/orders/:orderId', {
                templateUrl: 'views/show_order.html',
                controller: 'ShowOrderCtrl'
            })
            .otherwise({
                redirectTo: '/'
            })
    }]);

We need to define `ng-app` directive once. This becomes the placeholder for views. Each view referred by the route is loaded in this section of document.

You can define `ng-view` in main html file in the below way.

    <div ng-view></div>


### Pass Parameters in Route URLs

In Angular we can define parameters using `orderId` in URL.

    $routeProvider
        .when('/orders/:orderId', {
            templateUrl: 'views/show_order.html',
            controller: 'ShowOrderCtrl'
        })

We can read the parameter in ShowOrderCtrl by using `$routeParams.orderId`.

    $scope.orderId = $routeParams.orderId;

We can define HTML link as following:

    <a href="#/orders/1234">Show Details</a>

