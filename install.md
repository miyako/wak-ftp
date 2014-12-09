**How to create a global pointer to a modules installed in a non-standard location**

CommonJS Modules installed in the project's [Module](http://doc.wakanda.org/About-SSJS-Modules/Configuring-Custom-SSJS-Modules.200-953093.en.html) folder can be loaded with a simple [require](http://doc.wakanda.org/require.301-664756.en.html) statement.

However, you may want to store a certain module elsewhere, to share between multiple projects, multiple solutions, moultiple repositories, and so on. 

This document explains various ways to acheive this.

---

**Solution 1**: Use a dedicated project

Every modules follows your system's calling convention.

---

**Solution 2**: Use an absolute path to a location inside the solution

For example:
```
var ftp = require(solution.getFolder("path") + "Modules/ftp");
```
The advantage is that you can define a portable path relative to the solution. 

Note that the subpath (Modules/ in the example above) is hard-coded for each require call.

---

**Solution 3**: Define a filesystems.json at the solution or project level (my preference)

Create a [filesystems.js](http://doc.wakanda.org/Files-and-Folders/Customizing-FileSystem-Definitions.200-1037821.en.html), if you don't already have one, and define a location named "Modules".

The module can be anywhere on your file system, but it needs to be inside the solution for it to suface in the solution explorer.

For example, to define a location inside the solution:
```
  {
  "name":"Modules",
  "parent":"SOLUTION",
  "path":"Modules",
  "writable":true
  }  
```
The code to load a module inside this location would be:
```
var modulesFolder = FileSystemSync('Modules');
var ftp = require(modulesFolder.path + 'ftp');
```
The advantage is that the abstraction is created through filesystems.js, over which you have full control during development. (The filesystem is defined once when the solution is started.)

You are effectively passing an absolute path to require, which rules out ambiguity, but the advantage of a filesystem is that the module can be located anywhere, and moved around, by just changing the files system object. 

---

**Solution 4**: Define a custom location in [require.paths](http://doc.wakanda.org/Global-Application/Application/require.301-664756.en.html)

Create a **required.js** at the [solution](http://doc.wakanda.org/Architecture-of-Wakanda-Applications/Solution.200-1022674.en.html) or [project](http://doc.wakanda.org/Architecture-of-Wakanda-Applications/Project.200-1022680.en.html) level, if you don't already have one, and define a location search path with your preferred order of precedence.

The module can be anywhere on your file system, but it needs to be inside the solution for it to surface in the solution explorer.

For example, to define a location inside the solution:
```
require.paths.push(solution.getFolder("path")  + '/Modules/');
```
The code to load a module inside this location would be:
```
var ftp = require('ftp');
```
The advantage is that your require code would be clean and simple. The abstraction is created by required.js, over which you have full control at runtime. 

You do need to care about modules with the same name, installed in a search path with a higher precedence. For example, you can't require a module named "crpto", for example, because that name is already taken by a native module.

---
**Note**
The rules apply to CommonJS modules installed on the server side. Keep in mind that for a module to be published as an [RPC](http://doc.wakanda.org/Using-JSON-RPC-Services/Configuring-CommonJS-Modules-for-RPC.300-306585.en.html) service, it mustbe found in the standard location, the Modules folder of the project.

