MEAN Tutorial lesson 2

# Prerequisites

* MEAN Tutorial lesson 1

# Steps

## Packages

Create a file `db.js`

```javascript
module.exports = {
  url: 'mongo://localhost'
};
```

`require` the package at the top in the main script, use it and run the script:

```javascript
const db = require('./db.js');
.
.
.
log(`Initializing the application. Connected to '${db.url}'`);
```

Move the save function to the package:

```javascript
module.exports = {
  url: 'mongo://localhost',
  save: function (data, cb) {
    log('saving to db');
    // Code to save to the db will be here...
    setTimeout(function () {
      log(`Product id '${data.productId}' saved!`);
      cb('ok');
    }, 1000);
  }
};
```

Change the function utilization and run the script:

```javascript
db.save(data, callback);
```

Fix the log error passing the log object as a function parameter to the package:

```javascript
module.exports = function (log) {
  return {
    url: 'mongo://localhost',
    save: function (data, cb) {
      log('saving to db');
      // Code to save to the db will be here...
      setTimeout(function () {
        log(`Product id '${data.productId}' saved!`);
        cb('ok');
      }, 1000);
    }
  }
};
```

And passing the log in the require:

```javascript
const db = require('./db.js')(log);
```
