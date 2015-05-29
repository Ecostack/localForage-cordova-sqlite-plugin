localForage-cordova-sqlite-plugin
=================================

A cordova-sqlite-storage driver for [localForage](https://github.com/mozilla/localForage).

# Info
There are two drivers in this repository. 

- cordova-sqlite-plugin
- cordova-sqlite-plugin-no-support-check

The first one depends in the "checkSupport" method on the ["deviceready" event](http://docs.phonegap.com/en/4.0.0/cordova_events_events.md.html) of Cordova.

The second one just tells that the support is guaranteed everytime. The last was created due to a bug, that the "deviceready" event is sometimes not fired in Steroids and Ionic.

See these tickets for more information:

https://github.com/AppGyver/steroids/issues/772

https://github.com/driftyco/ionic-cli/issues/259

# Requirements

- localForage has to be loaded before this plugin
- cordova-sqlite-storage plugin has to be loaded

# Configuration
## Normal
TODO
## With Angular

With Angular you would first configure the localForageProvider.

It could look like this:
```
// Example
angular.module('<REPLACE_ME_WITH_MODULE_NAME>')
// The important part
// driver could be the single 'cordova-sqlite-plugin' or with some alternatives
// size can be defined, in this example 100mb
.config(['$localForageProvider', function($localForageProvider) {
	$localForageProvider.config({
		driver: ['asyncStorage',
			'cordova-sqlite-plugin',
			'webSQLStorage'
		],
		size: 100 * 1024 * 1024
	});
}])

// in the controller/service you could use it like this
.service('<REPLACE_ME_WITH_SERVICE_NAME>',
	function($localForage, $q) {
	  var lcReturn = {};
	  
	  lcReturn.get = function(pKey) {
		return $localForage.getItem(pKey);
	  };
		
		// other service methods..
	  
	  return lcReturn;
	
	});
	```
