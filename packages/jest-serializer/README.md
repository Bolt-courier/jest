# jest-serializer

> DEPRECATED: Use `v8` APIs directly: https://nodejs.org/api/v8.html#serialization-api

Module for serializing and deserializing object into memory and disk. The Node core `v8` implementations are used. This seriializer have the advantage of being able to serialize `Map`, `Set`, `undefined`, `NaN`, etc..

## Install

```sh
$ yarn add jest-serializer
```

## API

Three kinds of API groups are exposed:

### In-memory serialization: `serialize` and `deserialize`

This set of functions take or return a `Buffer`. All the process happens in memory. This is useful when willing to transfer over HTTP, TCP or via UNIX pipes.

```javascript
import {deserialize, serialize} from 'jest-serializer';

const myObject = {
  foo: 'bar',
  baz: [0, true, '2', [], {}],
};

const buffer = serialize(myObject);
const myCopyObject = deserialize(buffer);
```

### Synchronous persistent filesystem: `readFileSync` and `writeFileSync`

This set of functions allow to send to disk a serialization result and retrieve it back, in a synchronous way. It mimics the `fs` API so it looks familiar.

```javascript
import {readFileSync, writeFileSync} from 'jest-serializer';

const myObject = {
  foo: 'bar',
  baz: [0, true, '2', [], {}],
};

const myFile = '/tmp/obj';

writeFileSync(myFile, myObject);
const myCopyObject = readFileSync(myFile);
```
