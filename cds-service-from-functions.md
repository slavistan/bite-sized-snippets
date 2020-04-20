---
title: CDS Service Made From Functions
tags: cds cap
---

# Expose functions via a service

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
