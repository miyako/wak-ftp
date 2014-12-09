**How to create a global pointer to a modules installed in a non-standard location**

CommonJS Modules installed in the project's [Module](http://doc.wakanda.org/About-SSJS-Modules/Configuring-Custom-SSJS-Modules.200-953093.en.html) folder can be loaded with a simple [require](http://doc.wakanda.org/require.301-664756.en.html) statement.

However, you may want to store a certain module elsewhere, to share between multiple projects, multiple solutions, moultiple repositories, and so on. 

This document explains various ways to acheive this.

**Use a dedicated project** 

