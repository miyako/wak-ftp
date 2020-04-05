wak-ftp
=======

Wakanda FTP Module.

![obsolete-word-black-frame-word-obsolete-word-black-frame-d-rendering-123942590](https://user-images.githubusercontent.com/1725068/78463940-29122280-771e-11ea-8be8-a7830725403e.jpg)

Old Wakanda.

About
-----

The module includes [lftp](http://lftp.yar.ru) 4.6.0 executable for Mac, Windows x64, and Linux x64.

The executables for Mac are built with @loader_path and for Linux with $ORIGIN, so no need to install lftp, libiconv, libintl, libidn, libreadline, zlib, libgmp, libnettle, libhogweed or libgnutls.

* Note: The binaries for Mac and Linux were built from the standard GNU source code and uses gnutls. The binary for Windows were obtained from [here](http://nwgat.ninja/lftp-for-windows/) and uses OpenSSL. 

Install
-------
Please read [install](install.md).

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
