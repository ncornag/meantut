MEAN Tutorial lesson 1

# Prerequisites

* Node.js

```bash
brew install node
```

# Steps

Create a new folder:

```bash
mkdir tutorial
cd tutorial
```

## First script

Create a new file

```bash
vi index.js
```

Write to the file:

```javascript
console.log('Hello world');
```

Execute the program:

```bash
node index.js
```

or better:
```bash
npm i -g supervisor
supervisor index.js
```

## Functions

Create a function:

```javascript
function log(text){
  console.log(`info: ${text}`);
}
console.log('Hello world');
```

Modify the script to use the function and execute it:

```javascript
function log(text){
  console.log(`info: ${text}`);
}

log('Initializing the application');
```

## Callbacks

Create another function to simulate a "save" to a db:

```javascript
function log(text){
  console.log(`info: ${text}`);
}

function save(data, cb){
  log('saving to db');
  // Code to save to the db will be here...
  cb('ok');
}

log('Initializing the application');
```

Modify the script to use the function and execute it:

```javascript
function log(text){
  console.log(`info: ${text}`);
}

function save(data, cb){
  log('saving to db');
  // Code to save to the db will be here...
  cb('ok');
}

log('Initializing the application');

const data = { productId: '123456', title: 'Log title text' };

const callback = function(code) {
  log(`Save response: '${code}'`);
};

save( data, callback );

log('After save');
```

## ES6 (ES2015)

Convert the callback function to the new ES6 syntax:

```javascript
const callback = (code) => {
  log(`Save response: '${code}'`);
};
```

or, more concisely:

```javascript
const callback = (code) => log(`Save response: '${code}'`);

```

## Async functions

Simulate an async operation with setTimer in the `save` function and execute it:

```javascript
function save(data, cb){
  log('saving to db');
  // Code to save to the db will be here...
  setTimeout(function () {
    log(`Product id '${data.productId}' saved!`);
  }, 1000)
  cb('ok');
}
```

Fix the callback position and execute it:

```javascript
function save(data, cb){
  log('saving to db');
  // Code to save to the db will be here...
  setTimeout(function () {
    log(`Product id '${data.productId}' saved!`);
    cb('ok');
  }, 1000)
}
```
