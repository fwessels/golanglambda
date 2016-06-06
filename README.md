golanglambda
============

Run the AWS Javascript SDK as a VM in pure Go. It is based on [otto](https://github.com/robertkrimen/otto) as well as [ottoext](https://github.com/deoxxa/ottoext) (adapted and vendored for this version).

Building
--------

Use browserify to prepare your script, like this:
```
browserify sample-s3.js > sample-s3-browserified.js
```

Example
-------

```
$ golanglambda sample-s3-browserified.js
```
