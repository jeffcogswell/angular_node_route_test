This is two quick samples
* A router demo in Angular 
* A VERY simple node express app that for any HTML request, regardless of path, it *always* returns index.html.

**The idea is that regardless of path, we always return index.html, and routing always works, even when a full path is requested!** The browser-side angular library handles it correctly.
  
To run this:
1. Run ```ng build``` from within the front2 folder.
2. Copy the contents of dist/front2 into the backend/public folder.
3. Run ```npm start```. Do not run the angular server/app! Everything is served from the node app.

Then note the main app.js. It always returns **index.html** for regular html page requests *regardless of path*; see the app.get call below:

<pre>
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

<b>app.get('*', function(req, res, next) {
    res.sendFile('index.html', {root: path.join(__dirname, 'public') });
});
</b>
module.exports = app;
</pre>
