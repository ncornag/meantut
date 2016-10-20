MEAN Tutorial lesson 3

# Prerequisites

* MEAN Tutorial lesson 2

# Steps

## Use node packages

Add the `http` package and use it. Run the script and navigate to
`http://127.0.0.1:3000/save?productId=2` or any other url:

```javascript
const db = require('./db.js')(log);
const http = require('http');

function log(text) {
  console.log(`info: ${text}`);
}

log(`Initializing the application. Connected to '${db.url}'`);

http.createServer(function (request, response) {
  log(`Request received: ${request.url}`);
  response.writeHead(200, { 'Content-Type': 'text/plain' });
  response.end('Hello World\n');
}).listen(3000);

log('Server running at http://127.0.0.1:3000/');
```

## npm to install external packages

Create a `package.json`:

```bash
npm init
```

Tell npm to download a new package:

```bash
npm install --save express
```

or

```bash
npm i -S express
```

or use the new kid in the block:

```bash
npm i -g yarn
yarn add express
```

## Express use

Add express to the script and run it to navigate to `http://127.0.0.1:3000`,
`http://127.0.0.1:3000/save?productId=2` or any other url:

```javascript
const db = require('./db.js')(log);
const http = require('http');

function log(text) {
  console.log(`info: ${text}`);
}

log(`Initializing the application. Connected to '${db.url}'`);

const express = require('express');
const app = express();

app.get('/save', function (req, res) {
  log(`Request received: ${req.url}, saving product '${req.query.productId}'`);
  db.save(req.query, function (code) {
    res.send(`Product '${req.query.productId}' saved with code '${code}'`);
  });
});
app.get('/', function (req, res) {
  log(`Request received: ${req.url}`);
  res.send('Hello World!');
});

app.listen(3000, function () {
  log('Server running at http://127.0.0.1:3000/');
});
```

## Static files

Create a 'public/index.html':

```html
<html>
  <body>
  Hello world
  </body>
</html>
```

Tell express where to find the static files:

```javascript
.
.
.
app.use(express.static('public'));
app.listen(...)
```

Change the '/' route:

```javascript
app.get('/', function (req, res) {
  log(`Request received: ${req.url}`);
  res.redirect('/index.html');
});
```
