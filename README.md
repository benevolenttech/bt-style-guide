1. [Objects](#objects)


## Objects
Use the literal syntax for object creation. eslint: [`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)

```javascript
// bad
const item = new Object()

// good
const item = {}
```

Use computed property names when creating objects with dynamic property names.

> Why? They allow you to define all the properties of an object in one place.

```javascript

function getKey(k) {
  return `a key named ${k}`
}

// bad
const obj = {
  id: 5,
  name: 'San Francisco',
};
obj[getKey('enabled')] = true;

// good
const obj = {
  id: 5,
  name: 'San Francisco',
  [getKey('enabled')]: true,
};
```

Use object method shorthand. eslint: [`object-shorthand`](http://eslint.org/docs/rules/object-shorthand.html) jscs: [`requireEnhancedObjectLiterals`](http://jscs.info/rule/requireEnhancedObjectLiterals)

```javascript
// bad
const atom = {
  value: 1,

  addValue: function (value) {
    return atom.value + value
  },
};

// good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};
```

Use property value shorthand. eslint: [`object-shorthand`](http://eslint.org/docs/rules/object-shorthand.html) jscs: [`requireEnhancedObjectLiterals`](http://jscs.info/rule/requireEnhancedObjectLiterals)

> Why? It is shorter to write and descriptive.

```javascript
const lukeSkywalker = 'Luke Skywalker'

// bad
const obj = {
  lukeSkywalker: lukeSkywalker,
};

// good
const obj = {
  lukeSkywalker,
}
```

Group your shorthand properties at the beginning of your object declaration.

> Why? It's easier to tell which properties are using the shorthand.

```javascript
const anakinSkywalker = 'Anakin Skywalker'
const lukeSkywalker = 'Luke Skywalker'

// bad
const obj = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker,
}

// good
const obj = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4,
}
```

Only quote properties that are invalid identifiers. eslint: [`quote-props`](http://eslint.org/docs/rules/quote-props.html) jscs: [`disallowQuotedKeysInObjects`](http://jscs.info/rule/disallowQuotedKeysInObjects)

> Why? In general we consider it subjectively easier to read. It improves syntax highlighting, and is also more easily optimized by many JS engines.

```javascript
// bad
const bad = {
'foo': 3,
'bar': 4,
'data-blah': 5,
}

// good
const good = {
foo: 3,
bar: 4,
'data-blah': 5,
}
```

Do not call `Object.prototype` methods directly, such as `hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`.

> Why? These methods may be shadowed by properties on the object in question - consider `{ hasOwnProperty: false }` - or, the object may be a null object (`Object.create(null)`).

```javascript
// bad
console.log(object.hasOwnProperty(key))

// good
console.log(Object.prototype.hasOwnProperty.call(object, key))

// best
const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
/* or */
const has = require('has')
…
console.log(has.call(object, key))
```