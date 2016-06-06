golanglambda
============

Run the AWS Javascript SDK as a VM in pure Go. It is based on [otto](https://github.com/robertkrimen/otto) as well as [ottoext](https://github.com/deoxxa/ottoext) (adapted and vendored for this version).

Building
--------

Make sure you are using Go 1.6 so that the vendor directory is picked up, and do a `go install`.

Preparing a script
------------------

See the `sample_s3.js` for a test script. Edit it with your own credentials.

You will need to 'browserify' it in order to embed all `require`d modules, which is the next step  

### Install browserify

See [browserify](http://browserify.org/#install) for installation instructions.

Then make sure the modules that you want to use are installed locally. For the `sample_s3.js` you need to do the following

```
$ npm install aws-sdk
$ npm install node-uuid
```

Use browserify to prepare your script, like this:
```
browserify sample-s3.js > sample-s3-browserified.js
```

Example
-------

```
$ golanglambda sample-s3-browserified.js
```
