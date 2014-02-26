# angular-primus [![Build Status](https://travis-ci.org/neoziro/angular-primus.png?branch=master)](https://travis-ci.org/neoziro/angular-primus)

Primus service for Angular.

This plugin works with other Primus plugins like [primus-emitter](https://github.com/cayasso/primus-emitter) and [primus-resource](https://github.com/cayasso/primus-resource).

## Install

### Using bower

```js
bower install angular-primus
```

## Usage

```js
angular.module('controllers.primus', ['primus'])
.config(function (primusProvider) {
  // Configure Primus.
  primusProvider
  .setEndpoint('http://mywebsite.com')
  .setOptions({
    reconnect: {
      minDelay: 100,
      maxDelay: 60000,
      retries: 100
    }
  });
})
.controller('PrimusCtrl', function ($scope, primus) {

  // Listen "data" event.
  primus.$on('data', function (data) {
    $scope.data = data;
  });

  // Write data.
  primus.write('hello');


  // Listen custom event using primus-emitter.
  primus.$on('customEvent', function (customData) {
    $scope.customData = customData;
  });

  // Send data using primus-emitter.
  primus.send('customEvent', { foo: 'bar' });


  // Use resource with primus-resource.
  primus.$resource('myResource').then(function (myResource) {
    myResource.myMethod();
  });
});
```

## License

MIT