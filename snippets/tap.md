---
title: tap
tags: object,advanced
---

Allows to call any method of an object and always return the object passed to the tap function, regardless of what the method actually returns in its definition.

- Creates a `Proxy` to intercept methods call and return the given object.

```js
const tap = subject => {
  return new Proxy({}, {
    get(target, method) {
      return (...args) => {
        subject[method](...args);

        return subject;
      };
    }
  });
}
```

```js
const obj = { foo: () => 'bar' };

obj.foo(); // returns "bar"
tap(obj).foo() // returns {foo: ƒ}
```
