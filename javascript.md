https://gist.github.com/Ak-Shaw/360b4ec2a19c4e94cc2dcf0874d4eae2

Sealing an object globally
Property descriptors work at the level of individual properties.

There are also methods that limit access to the whole object:

Object.preventExtensions(obj)
Forbids the addition of new properties to the object.
Object.seal(obj)
Forbids adding/removing of properties. Sets configurable: false for all existing properties.
Object.freeze(obj)
Forbids adding/removing/changing of properties. Sets configurable: false, writable: false for all existing properties.
And also there are tests for them:

Object.isExtensible(obj)
Returns false if adding properties is forbidden, otherwise true.
Object.isSealed(obj)
Returns true if adding/removing properties is forbidden, and all existing properties have configurable: false.
Object.isFrozen(obj)
Returns true if adding/removing/changing properties is forbidden, and all current properties are configurable: false, writable: false.
