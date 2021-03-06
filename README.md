# Astatine
Astatine - A Small Ajax and HTML Form Library. Library entry point. Globally available by using `Astatine` or `At`.


## Overview
- 3KB uncompressed
- Install `npm install astatine`
- Link `astatine.min.js`
- ES5 browsers and up. (Probably older ones but who cares about those)

## TODO
- File Upload


## API


### Astatine.setup.spinner
Sets up spinner color, thickness, and size. Defaults are listed bellow. Do this before any Astatine or At operations.

##### Example
```JavaScript
Astatine.setup.spinner.size = '3px';
Astatine.setup.spinner.thickness = '15px';
Astatine.setup.spinner.colorTop = 'darkgray';
Astatine.setup.spinner.colorBottom = 'lightgray';
```


### Astatine.submit(options)
Listens on a form element for submit event to be fired.

##### Special Features
- `radio` will only appear if it is checked.
- `checkbox` will either be `true` or `false`.
- `type="submit"` will automatically hide. And a spinner will show on submit.
- `.spinner` will automatically created and make visible a spinner.

##### Options
The options object accepts all items form the `Astatine.ajax` method. Please review that section for more detail.

- `action: String` Resource action url. **Required**
- `query: String | Element` Query selector or element. **Required**
- `method: String` Valid methods get, post, put, delete. **Required**

- `reset: Boolean` Resets form after submit success. Defaults to true.

- `complete: Function` Parameters are the XHR. **Required**
	- `error` An xhr object
	- `success` An xhr object

- `prepare: Function` Allows the ability to edit/validate the option.data object before complete/post.
	- `data: Object` The form data object.
	- `resolve: Function` Async resolve function requires the data as a parameter.
	- `reject: Function` Async reject passes its parameter to the complete function as an error.

##### Example
```HTML
<form class="form" method="post" action="/post/path">
	<input type="text" name="name" placeholder="Name" required>
	<input type="submit" value="Submit"/>
</form>
```
```JavaScript
Astatine.submit({
	query: '.form',
	prepare: function (data, resolve, reject) {
		data.foo = 'bar'; // manipulate data before send

		// return data;

		setTimeout(function () {
			if (true) resolve(data); // async resolve
			else reject({ response: 'rejected' }); // async reject
		}, 1000);

	},
	complete: function (error, success) {
		if (error) console.log(error);
		else console.log(success);
	}
});
```


### Astatine.ajax(options)
Ajax is a lower level utility function that allows for more control but less features than the submit method.

##### Options
- `action: String` Resource action url. **Required**
- `method: String` Valid methods get, post, put, delete. **Required**

- `success: Function` **Required**
- `error: Function` **Required**

- `data: Object` If method is `GET` than data is concatenated to the `action/url` as parameters.

- `requestType: String` Converts the request data before sending.
	- `script` 'text/javascript, application/javascript, application/x-javascript'
	- `json` 'application/json' stringify `options.data`
	- `xml` 'application/xml, text/xml'
	- `html` 'text/html'
	- `text` 'text/plain'
	- DEFAULT 'application/x-www-form-urlencoded' serialized `options.data`

- `responseType: String` Converts the response data after sending.
	- `script` 'text/javascript, application/javascript, application/x-javascript'
	- `json` 'application/json'
	- `xml` 'application/xml, text/xml'
	- `html` 'text/html'
	- `text` 'text/plain'

- `contentType: String` Short hand to set the Content-Type Headers. (For request)
- `accept: String` Short hand to set the Accept Headers. (For response)

- `mimeType: String` Overwrites return type.
- `username: String`
- `password: String`
- `withCredentials: Boolean`
- `headers: Object`    A low level headers object it will map directly to the XHR header. The Will overwrite any above options.

##### Example
```JavaScript
Astatine.ajax({
	method: 'get',
	action: '/examples/index.html',
	data: { name: 'stuff' },
	success: function (xhr) {
		console.log(xhr);
	},
	error: function (xhr) {
		console.log(xhr);
	}
});
```


### Astatine.formData(element)

##### Parameter
- `Object` DOM element

##### Example
```JavaScript
var objectData = Astatine.formData(element);
```


### Astatine.serialize(data)

##### Parameter
- `Object` Single level deep key value pare

##### Example
```JavaScript
var stringData = Astatine.serialize(data);
```


## License
Licensed Under MPL 2.0
Copyright 2016 [Alexander Elias](https://github.com/AlexanderElias/)
