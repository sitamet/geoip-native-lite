# geoip-native-lite

Super-fast IP to country lookups with minimal RAM usage.

[![Build Status](https://travis-ci.org/chill117/geoip-native-lite.svg?branch=master)](https://travis-ci.org/chill117/geoip-native-lite) [![Status of Dependencies](https://david-dm.org/chill117/geoip-native-lite.svg)](https://david-dm.org/chill117/geoip-native-lite)


## Goals

* Fast IP address to country lookup:
  * 1,000,000+ ops/second for IPv4 addresses
  * 500,000+ ops/second for IPv6 addresses
* Minimal RAM usage
* Native JavaScript implementation for ease-of-use and portability


## Installation

Add to your application via `npm`:
```
npm install geoip-native-lite --save
```
This will install `geoip-native-lite` and add it to your application's `package.json` file.


## Update Data Files

This module ships with pre-built data files. If you'd like to update the data files for yourself, run the update script like this:
```
npm run updatedata
```


## How to Use

* [lookup](#lookup)
* [loadData](#loaddata)
* [loadDataSync](#loaddatasync)

### lookup

`lookup(ip)`

Lookup the country in which the IP address is located. Supports both ipv4 and ipv6.

Usage:
```js
var GeoIpNativeLite = require('geoip-native-lite');

// Must load data before lookups can be performed.
GeoIpNativeLite.loadDataSync();

// Data loaded successfully.
// Ready for lookups.
var ip = '128.21.16.34';
var country = GeoIpNativeLite.lookup(ip);

if (country) {
	console.log(ip, 'is geo-located in', country.toUpperCase());
} else {
	console.log('Failed to geo-locate the IP address:', ip);
}
```


### loadData

`loadData([options, ]cb)`

Asynchronously loads geoip data.

Usage:
```js
var GeoIpNativeLite = require('geoip-native-lite');

GeoIpNativeLite.loadData(options, function(error, data) {

	if (error) {
		// Something went wrong.
	} else {
		// Data loaded successfully.
		// Ready for lookups.
	}
});
```

Options:
```js
var options = {

	/*
		Set to TRUE to load ipv4 geoip data.

		Default value is TRUE.
	*/
	ipv4: true,

	/*
		Set to TRUE to load ipv6 geoip data.

		Default value is FALSE.
	*/
	ipv6: false,

	/*
		Set to TRUE to cache data in memory.

		Default value is TRUE.
	*/
	cache: true
};
```

### loadDataSync

`loadDataSync([options])`

Synchronously loads geoip data.

Usage:
```js
var GeoIpNativeLite = require('geoip-native-lite');

GeoIpNativeLite.loadDataSync(options);

var country = GeoIpNativeLite.lookup('198.169.246.30');
```

Options:
```js
var options = {

	/*
		Set to TRUE to load ipv4 geoip data.

		Default value is TRUE.
	*/
	ipv4: true,

	/*
		Set to TRUE to load ipv6 geoip data.

		Default value is FALSE.
	*/
	ipv6: false,

	/*
		Set to TRUE to cache data in memory.

		Default value is TRUE.
	*/
	cache: true
};
```


## Contributing

There are a number of ways you can contribute:

* **Improve or correct the documentation** - All the documentation is in this `readme.md` file. If you see a mistake, or think something should be clarified or expanded upon, please [submit a pull request](https://github.com/chill117/geoip-native-lite/pulls/new)
* **Report a bug** - Please review [existing issues](https://github.com/chill117/geoip-native-lite/issues) before submitting a new one; to avoid duplicates. If you can't find an issue that relates to the bug you've found, please [create a new one](https://github.com/chill117/geoip-native-lite/issues).
* **Request a feature** - Again, please review the [existing issues](https://github.com/chill117/geoip-native-lite/issues) before posting a feature request. If you can't find an existing one that covers your feature idea, please [create a new one](https://github.com/chill117/geoip-native-lite/issues).
* **Fix a bug** - Have a look at the [existing issues](https://github.com/chill117/geoip-native-lite/issues) for the project. If there's a bug in there that you'd like to tackle, please feel free to do so. I would ask that when fixing a bug, that you first create a failing test that proves the bug. Then to fix the bug, make the test pass. This should hopefully ensure that the bug never creeps into the project again. After you've done all that, you can [submit a pull request](https://github.com/chill117/geoip-native-lite/pulls/new) with your changes.


## Tests

To run all tests (except benchmarks):
```
npm test
```

To run benchmarks:
```
npm run test:benchmarks
```

To run only unit tests:
```
npm run test:unit
```

To run only code-style checks:
```
npm run lint
```


## Licensing

All the code in this project is [MIT licensed](https://github.com/chill117/geoip-native-lite/blob/master/LICENSE).

The geoip data used in this project is [licensed separately](https://github.com/chill117/geoip-native-lite/blob/master/data/LICENSE.txt).
