---
title: CDS Snippets
tags: cds cap
---

#### Exposing a function

```cds
/* 📁 srv/test-srv.cds */
service TestSrv {
  /*
   * Echo input. 
   * Usage: GET http://localhost:4004/test-srv/echo(msg='asdf')
   */
  function echo (msg : String) returns String;

  /*
   * Print server time.
   * Usage: GET http://localhost:4004/test-srv/srvtime()
   */
  function srvtime() returns DateTime;
}
```

```js
/* 📁 srv/test-srv.js */
module.exports = function(srv) {
  srv.on ('echo', req => `${req.data.msg}`)

  srv.on ('srvtime', req => {
    /* Returns Edm.DateTimeOffset */
    var x = new Date().toISOString()
    return x
  })
}
```

---

#### Manual Routing Of Services

**tl;dr** At service definition use the *path* decorator `@(path: '/mypath')` to manually route a service. The default path corresponds to the source file name.

```cds
service MyService @(path: '/mysrv') {
  // ...
}
```

