# Trailing coma immutability

Trailing coma after last element in arrays and objects literals can specify, that literal is mutable, or extencible

Currently this have very unusable sense, which reflect only code style conventions, but can be switched to practical logic sense

In the next example showed immutable behavior:
```javascript
let mutableObject = {
  field1: 'value-1',
  field2: 'value-2', // this coma mark object as mutable
};

// this is works normal
mutableObject.field1 = 'other-value'; 

let immutableObject = {
  field1: 'value-1',
  field2: 'value-2'  // no trailing coma mark object as immutable
};

// throw "Can not mutate immutable literal" error
immutableObject.field1 = 'other-value'; 

// common immutable objects usage example
let newImmutableState = Object.assign(immutableObject, {
  field1: 'other-value'
});
```
