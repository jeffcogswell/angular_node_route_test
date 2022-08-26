This is two quick samples
* A router demo in Angular 
* A VERY simple node express app that for any HTML request, regardless of path, it *always* returns index.html.
  
After  ```ng build``` I copied all the dist files into the node app's public folder.

Then note the main app.js. It always returns index.js for regular html page requests:

```js
var express = require('express');
var path = require('path');
var cookieParser = require('cookie-parser');
var logger = require('morgan');

var app = express();

app.use(logger('dev'));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, 'public')));

app.get('*', function(req, res, next) {
	res.sendFile('index.html', {root: path.join(__dirname, 'public') });
});

module.exports = app;
```
