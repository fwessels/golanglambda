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

### Patch AWS SDK

For now we need to patch the AWS Javascript SDK to use a `fetch` object instead of the standard `XMLHttpRequest` object. You can do this as follows:

```
$ cd node_modules/aws-sdk/lib/http
$ wget https://raw.githubusercontent.com/fwessels/aws-sdk-js/324d927a278a551264f0d6c2078d852bb7ed2416/lib/http/xhr.js
```


After this you can use browserify to prepare your script for running by golanglambda, and we need to make one more modification to prevent an 'old browser' warning (still to be fixed).

```
$ browserify sample_s3.js | sed 's/= oldBrowser$/= function\(size, cb\) \{ return new Buffer\(size\) \}/' > sample_s3-browserified.js
```

Example
-------

After this you can run your sample:

```
$ golanglambda sample-s3-browserified.js
```
