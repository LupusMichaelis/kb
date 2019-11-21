# AngularJS

*Beware: AngularJS isn't Angular. The latter is a rewrite in Typescript of the former!*

[Tutorial](https://www.w3schools.com/angular/angular_intro.asp)
[Tutorial showcase](https://www.w3schools.com/angular/angular_w3css.asp)
[API reference](https://docs.angularjs.org/api/ng/)

## Global tools

Angular exposes a bunch of helper on its root object. Might be better to use a general
purpose libraty (like lodash) for this kind of usage.

## Directives

* `ng-app`:     root element
* `ng-init`:    initial values
* `ng-model`:   bind an input element to a value
* `ng-bind`:    bind an element to a value

## Instruction

* `ng-repeat`
* `ng-if`
* `ng-show`
* `ng-options`

## App cog factories

* `app.controller`
* `app.directive`
* `app.filter`
* `app.service`

## Basic component

```
<super-tag />                   <!-- Restrict with restrict: "E" -->
<div super-tag />               <!-- Restrict with restrict: "A" -->
<div class='super-tag' />       <!-- Restrict with restrict: "C" -->
<!-- directive: super-tag -->   <!-- Restrict with restrict: "M" -->
```

```
var app = angular.module("superApp", []);
app.directive("superTag", function() {
  return {
    restrict: "E", // Default "EA"
    template : "<h1>Made by a directive!</h1>"
  };
});
```

## Form

[Details](https://www.w3schools.com/angular/angular_validation.asp)

Classes are defined and can be defined to have a more user-friendly XP.

Binded input elements are decorated:

* `$dirty`: was the data altered in any way
* `$invalid`
* `$pristine`
* `$touched`
* `$touched`: was the data inspected by the user
* `$untouched`
* `$valid`: does the data validate the expected requirements

Form get state as well:

* `$dirty`
* `$invalid`
* `$pristine`
* `$submitted`
* `$valid`

Angular will add classes to input elements depending upon their status:

* `ng-dirty`
* `ng-empty`
* `ng-invalid`
* `ng-not-empty`
* `ng-pending`
* `ng-pristine`
* `ng-touched`
* `ng-untouched`
* `ng-valid`

## Filters

`{{wallet | currency}}`

## Services

Services are the variables passed to controller constructors.

* `$http`
* `$interval`
* `$location`

## Ajax

[HTTP](https://www.w3schools.com/angular/angular_http.asp)

## Events

Take an expression where `$event` is defined.

* `ng-blur`
* `ng-change`
* `ng-click`
* `ng-copy`
* `ng-cut`
* `ng-dblclick`
* `ng-focus`
* `ng-keydown`
* `ng-keypress`
* `ng-keyup`
* `ng-mousedown`
* `ng-mouseenter`
* `ng-mouseleave`
* `ng-mousemove`
* `ng-mouseover`
* `ng-mouseup`
* `ng-paste`

## Templating

`ng-include`

## Routing

`ng-route`

```
<ng-view />
<script src="//ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular-route.js"></script>
<script>
var app = angular
    .module("myApp", ["ngRoute"])
    .controller('HomeCtrl', function($scope) {})
    ;

app.config(function($routeProvider) {
    $routeProvider
        .when('/', { templateUrl: 'home.html', controller: 'HomeCtrl' })
        .when('/about', { template: '<p>About thing</p>', controller: 'AboutCtrl' })
        .otherwise({ template: '404' });
})
</script>
```
