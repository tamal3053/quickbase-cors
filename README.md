quickbase-cors
==============

[![npm license](https://img.shields.io/npm/l/quickbase.svg)](https://www.npmjs.com/package/quickbase-cors) [![npm version](https://img.shields.io/npm/v/quickbase.svg)](https://www.npmjs.com/package/quickbase-cors) [![npm downloads](https://img.shields.io/npm/dm/quickbase.svg)](https://www.npmjs.com/package/quickbase-cors)

---

### Originally Developed by Tristian Flanagan -> [tflanagan](https://github.com/tflanagan)

---

A lightweight, very flexible QuickBase API

[API Documentation](https://github.com/tflanagan/node-quickbase/blob/master/documentation/api.md)

[PHP Version](https://github.com/tflanagan/php-quickbase)

Install
-------
```
# Latest Stable Release
$ npm install quickbase-cors
```

Browserify
----------
To use the Browserify version go to : https://github.com/tflanagan/node-quickbase

Example
-------
```javascript
import QuickBase from "quickbase-cors";

const quickbase = new QuickBase({
    proxy: 'http://localhost',
    post: '1337',
	realm: 'www',
	appToken: '*****',
	// userToken: '*****'
});

// If using user tokens, you do not need to call API_Authenticate

/* Promise Based */
quickbase.api('API_Authenticate', {
	username: '*****',
	password: '*****'
}).then((result) => {
	return quickbase.api('API_DoQuery', {
		dbid: '*****',
		clist: '3.12',
		options: 'num-5'
	}).then((result) => {
		return result.table.records;
	});
}).each((record) => {
	return quickbase.api('API_EditRecord', {
		dbid: '*****',
		rid: record[3],
		fields: [
			{ fid: 12, value: record[12] }
		]
	});
}).then(() => {
	return quickbase.api('API_DoQuery', {
		dbid: '*****',
		clist: '3.12',
		options: 'num-5'
	});
}).then((result) => {
	console.log(result);
}).catch((err) => {
	console.error(err);
});
```

License
-------
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.