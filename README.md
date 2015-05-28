localForage-cordova-sqlite-plugin
=================================

A cordova-sqlite-storage driver for [localForage](https://github.com/mozilla/localForage).


# Requirements

- localForage has to be loaded before this plugin
- cordova-sqlite-storage plugin has to be loaded

# Configuration
## Normal

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
			return $q(function(resolve, reject) {
					$localForage.getItem(pKey).then(function(pItem) {
						resolve(pItem);
					}, function(pErr) {
						reject(pErr);
					})
			})
		}
		
		// other service methods..
	  
	  return lcReturn;
	
	});
	```
