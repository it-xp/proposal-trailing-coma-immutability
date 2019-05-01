# Trailing coma immutability

Trailing coma after last element in arrays and objects literals can specify, that literal is mutable, or extencible

Currently this have very unusable sense, which reflect only code style conventions, but can be switched to practical logic sense

In the next example showed immutable behavior:
```javascript
/* General concept: */

let mutableObject = {
  property1: 'value-1',
  property2: 'value-2', // this coma mark object as mutable
};

// this is works normal
mutableObject.property1 = 'other-value'; 
mutableObject.property3 = 'value-3'; 

let immutableObject = {
  property1: 'value-1',
  property2: 'value-2'  // no trailing coma mark object as immutable
};

// throw "Can not mutate immutable literal" error
immutableObject.property1 = 'other-value';
immutableObject.property3 = 'value-3';

// common immutable objects usage example
let newMutableState = Object.assign(immutableObject, {
  property1: 'other-value',
  property3: 'value-3', // trailing coma in assigned value mark result as mutable
});

// works
newMutableState.property1 = 'new value';

let newImutableState = Object.assign(immutableObject, {
  property1: 'other-value',
  property3: 'value-3'  // no trailing coma in assigned value mark result as immutable
});

// throw
newImmutableState.property1 = 'new value';

/* Switching object mutability */

// from immutable to mutable
mutabilitySwitchableObject = Object.assign(mutabilitySwitchableObject, {,});

// from mutable to immutable
mutabilitySwitchableObject = Object.assign(mutabilitySwitchableObject, {});

/* Combined or partial mutabiliti */

let combinedMutabilityObject = {
  mutableField: {
    immutableField: {
      property: 'value' // immutable
    }, // mutable
  },
  immutableField: {
    mutableField: {
      property: 'value', // mutable
    } // immutable
  } // immutable
}

// throw
combinedMutabilityObject.newProperty = 'new value';
combinedMutabilityObject.mutableField = 'new value';
combinedMutabilityObject.mutableField.immutableField.property = 'new value';
combinedMutabilityObject.immutableField.property = 'new value';

let somePointer = combinedMutabilityObject.immutableField;
somePointer.property = 'new value';

// works
combinedMutabilityObject.mutableField.newProperty = 'new value';
combinedMutabilityObject.immutableField.mutableField.property = 'new value';

let otherPointer = combinedMutabilityObject.immutableField.mutableField;
otherPointer.property = 'new value';

```
