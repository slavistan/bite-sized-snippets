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

---

#### Different Query Syntaxes

```js
/* "Fluent API" */
await SELECT.from(cds.entities.Cards)

/* Crud API */
await cds.read(cds.entitites.Cards)

/* CQL API */
await cds.run(cds.parse.cql('SELECT * FROM vizn_Cards'))
```

---

#### Pseudo-Automatic Deep Insert of Defaults


```cds
// db/service.cds

entity Cards {
    key ID: UUID;
    command: String;
    schedule: Composition of one Schedules on schedule.card=$self; // <-- DOES NOT work with Association of. Why?
}

entity Schedules {
    key ID: UUID;
    card: Association to Cards; // <-- MUST NOT be declared 'not null'. Stupid.
    asdf: Integer default 1337;
}

// Project data model to service
// ...
```

```http
POST http://localhost:4004/cards/Cards
Content-Type: application/json

{
  "command": "Hi",
  "schedule": {} // <-- MUST be included to generate a default schedule. Stupid.
}
```
