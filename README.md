jQuery File Upload Middleware [![Build Status](https://drone.io/github.com/Turistforeningen/node-jfum/status.png)](https://drone.io/github.com/Turistforeningen/node-jfum/latest)
=============================

[![NPM](https://nodei.co/npm/jfum.png?downloads=true)](https://www.npmjs.org/package/jfum)

`Warning` this module is currently in active development and will change without
notice!

## Features

* Bare minimal – no extra stuff
* Made for Express 4.x

## Requirements

* Node.JS >= 0.10
* Express >= 4

## Install

```
npm install jfum --save
```

## Usage

```javascript
var JFUM = require('JFUM');
var jfum = new JFUM({
  tmpDir: '/tmp',
  minFileSize: 204800,  // 200 kB
  maxFileSize: 5242880, // 5 mB
  acceptFileTypes: /\.(gif|jpe?g|png)$/i
});
```

### OPTIONS

jQuery File Upload makes an OPTIONS request to the server before starting the
uppload to make sure that it can upload to the given server.

```javascript
app.options('/upload', jfum.optionsHandler.bind(jfum));
```

### POST

```javascript
app.post('/upload', jfum.postHandler.bind(jfum), function(req, res) {
  for (var i = 0; i < req.jfum.files.length; i++) {
    var file = req.jfum.files[i];
    if (typeof file === 'object' && typeof file.error === 'undefined') {
      // file.path - full path to file
      // file.name - original file name
      // file.size - file size on disk
      // file.mime - file mime type
    } else {
      // the file was rejected or not uploaded correctly
      // error message will be in req.jfum.error
    }
  }
});
```

