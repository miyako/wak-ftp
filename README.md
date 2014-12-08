wak-ftp
=======

Wakanda FTP Module.

About
-----

The module includes [lftp](http://lftp.yar.ru) 4.6.0 executable for Mac, Windows x64, and Linux x64.

The executables for Mac are built with @loader_path and for Linux with $ORIGIN, so no need to install lftp, libiconv, libintl, libidn, libreadline, zlib, libgmp, libnettle, libhogweed or libgnutls.

* Note: The binaries for Mac and Linux were built from the standard GNU source code, and uses libgnutls. The binary for Windows were obtained from [here](http://nwgat.ninja/lftp-for-windows/) and uses OpenSSL. 

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
