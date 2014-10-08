# (Unofficial) "Pin It" Pinterest API

This is an unofficial interface to Pinterest's pin-it api.  You can pin anything you want to your own boards programatically using nodejs!

__Note:__ Pinterest _could_ change their api at any time causing this library to break.  You've been warned.

## Installation

### From the command line

```npm install pin-it-node```

### In package.json


```
{
	dependencies: {
		"pin-it-node": "~0.1.0"
	}
}
```

## Usage

<em>To Pin:</em>

```
var PinIt = require('pin-it-node');

var pinIt = new PinIt({
	username: 'MyUsername',
	password: 'MySuperSecretPassword'
});

pinIt.pin({
	boardId: '123',
	url: 'http://www.kengoldfarb.com', // The click back link from pinterest
	description: 'Wow.  Such dev.',
	media: 'http://www.kengoldfarb.com/images/pin-it.png' // The actual image that will be pinned
}, function(err, pinObj) {
	if(err) {
		// Uh-oh...handle the error
		console.log(err);
		return;
	}

	console.log('Success!  New pin has been added to the board.');
	console.log(pinObj);
})
```

<em>To Remove Pin:</em>

```
var PinIt = require('pin-it-node');

var pinIt = new PinIt({
	username: 'MyUsername',
	password: 'MySuperSecretPassword'
});

pinIt.unpin({
	pinId: '123'
}, function(err, pinObj) {
	if(err) {
		// Uh-oh...handle the error
		console.log(err);
		return;
	}

	console.log('Success!  Pin has been removed from the board.');
	console.log(pinObj);
})
```

<em>To Edit Pin:</em>

```
var PinIt = require('pin-it-node');

var pinIt = new PinIt({
	username: 'MyUsername',
	password: 'MySuperSecretPassword'
});

pinIt.repin({
	boardId: '123',
	pinId: '12345', 
	userurl: 'kentester24', //the location of the user on Pinterest
	boardname: 'test-board', //the location of the board on Pinterest
	url: 'http://www.kengoldfarb.com', // The click back link from pinterest
	description: 'Wow.  Such dev.',
	
}, function(err, pinObj) {
	if(err) {
		// Uh-oh...handle the error
		console.log(err);
		return;
	}

	console.log('Success!  The pin has been edited.');
	console.log(pinObj);
})
```

__Currently only pinning of images is supported__

### Getting the boardId

You can get the boardId by going to pinterest and inspecting the GET request to http://www.pinterest.com/resource/BoardResource/get/.  You should see it listed in the "module_path" parameter of the request in the format: ```resource=BoardResource(board_id=1234567)```

### Getting the pinId
(for pin removal)
It's easy to grab from the html of the board.  Look for the href in the '.pinImageWrapper' class.  If you are viewing a pin, the pinId is the number in the url.

## Advanced Options

### 'request' module options

This module makes all it's http(s) requests using [request](https://github.com/mikeal/request).  You can optionally pass in a set of options for this module when making a request.

For example...

```
var PinIt = require('pin-it-node');

var pinIt = new PinIt({
	username: 'MyUsername',
	password: 'MySuperSecretPassword',
	requestDefaults: {
		proxy:'http://127.0.0.1:8888',
        strictSSL: false
	}
});

pinIt.pin({
	...
});
```

Consult the [request](https://github.com/mikeal/request) module documentation for a full list of options.

### debug mode

When instantiating set ```options.debug = true``` for more verbose log output.

```
var PinIt = require('pin-it-node');

var pinIt = new PinIt({
	username: 'MyUsername',
	password: 'MySuperSecretPassword',
	debug: true
});

...

```

## Versioning

This project will follow the [Semantic Versioning 2.0.0](http://semver.org/) guidelines once version 1.0.0 is released.  Until that time, any updates might be backwards-incompatible changes.

Since this is an unofficial api, a "stable" version 1.0.0 will be released once this has been tested in the wild and includes reasonable unit testing.

## Unit tests

__Not yet complete.__

To run the tests...

```
$ cd tests/
$ npm install
$ node_modules/.bin/mocha pinItTests.js
```

## Author

__Ken Goldfarb__ http://www.kengoldfarb.com

Contributed unpin and repin functions:  
__Ben Pevsner__ http://www.benpevsner.com

## License

MIT.  Do whatever you want with it.
