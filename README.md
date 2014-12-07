wak-ftp
=======

Wakanda FTP Module.

About
-----

The module includes [lftp](http://lftp.yar.ru) 4.6.0 executable for Mac and ~~Windows x64~~, 4.5.6 for Linux x64.

The executables for Mac are built with @loader_path and for Linux with $ORIGIN, so no need to install lftp, libiconv, libintl, libidn, libreadline, zlib, libgmp, libnettle, libhogweed or libgnutls.

Install
-------
The module can be installed in any solution.

* Create a solution level filesystems.js, if you don't already have one, and follow the example.
```
  {
  "name":"Modules",
  "parent":"SOLUTION",
  "path":"Modules",
  "writable":true
  }  
```

That' it!

Example
-------
```
var modulesFolder = FileSystemSync('Modules');
var ftp = require(modulesFolder.path + 'ftp');

var code = '';
code += 'open ftp://ftp.4d.com\n';
code += 'lcd ~/Downloads/\n';
code += 'get Favicon.ico\n';
code += 'bye\n';

ftp.ftp(code);
```
