# Astatine
Astatine || At - Simple Small Ajax and HTML Form Library


## Browser Support
ES5 supported browsers and up. Probably older ones but who cares about those.


## API

### Astatine || At
Library entry point. Globally use **At** or **Astatine**


### At.setup
#### At.setup.spinner
Sets up spinner color, thickness, and size. Defaults are listed bellow. Do this before any Astatine or At operations.

##### Usage
```JavaScript
At.setup.spinner.size = '3px';
At.setup.spinner.thickness = '15px';
At.setup.spinner.colorTop = 'darkgray';
At.setup.spinner.colorBottom = 'lightgray';
```


### At.submit
#### At.submit(options)
Submit form. Error and Success are your XHR response. Creates a spinner with the class `.spinner` and hides `type=submit`.

##### Features
- `application/json` automatically stringiifed to json string.
- `application/x-www-form-urlencoded` automatically serialized to url params.

##### Options
- **query**: `String` Query selector to form element
- **\***: Any `At.ajax` options

```html
<form class="form-contact" method="POST" enctype="application/json" action="/examples/index.html">
	<input type="text" name="name" placeholder="Name:" required/>
	<input type="submit" value="Submit"/>
</form>
```

```JavaScript
At.submit({
	query: '.form-contact',
	prepare: function (data) {
		data.foo = 'bar'; // manipulate data before send
	},
	complete: function (error, success) {
		if (error) console.log(error);
		else console.log(success);
	}
});
```


### At.ajax
#### At.ajax(options)
Ajax is a lower level utility function that allows for more control but less features than the submit method.

##### Options
- **enctype**: `String` Overwrites 'content-type' in headers
- **method**: `String` Valid methods get, post, put, and delete
- **action**: `String` Resource url
- **username**: `String`
- **password**: `String`
- **mimeType**: `String` Overwrites return type
- **data**: `Object` If method is `GET` than data is concatenated to the `action/url` as params
- **headers**: `Object`
- **prepare**: `Function`
- **complete**: `Function`

```JavaScript
At.ajax({
	data: { name: 'stuff' }, // params or data
	method: 'get', // post put delete
	action: '/examples/index.html',
	success: function (xhr) {
		console.log(xhr);
	},
	error: function (xhr) {
		console.log(xhr);
	}
});
```


### At.formData
#### At.formData(element)

##### Parameter
- `Object` DOM element

```JavaScript
var objectData = At.formData(element);
```


### At.serialize
#### At.serialize(data)

##### Parameter
- `Object` Single level deep key value pare

```JavaScript
var stringData = At.serialize(data);
```
