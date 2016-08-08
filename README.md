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
}

obj[getKey('enabled')] = true

// good
const obj = {
  id: 5,
  name: 'San Francisco',
  [getKey('enabled')]: true,
}
```

Use object method shorthand. eslint: [`object-shorthand`](http://eslint.org/docs/rules/object-shorthand.html) jscs: [`requireEnhancedObjectLiterals`](http://jscs.info/rule/requireEnhancedObjectLiterals)

```javascript
// bad
const atom = {
  value: 1,

  addValue: function (value) {
    return atom.value + value
  },
}

// good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value
  },
}
```

Use property value shorthand. eslint: [`object-shorthand`](http://eslint.org/docs/rules/object-shorthand.html) jscs: [`requireEnhancedObjectLiterals`](http://jscs.info/rule/requireEnhancedObjectLiterals)

> Why? It is shorter to write and descriptive.

```javascript
const lukeSkywalker = 'Luke Skywalker'

// bad
const obj = {
  lukeSkywalker: lukeSkywalker,
}

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
const has = Object.prototype.hasOwnProperty // cache the lookup once, in module scope.
/* or */
const has = require('has')
…
console.log(has.call(object, key))
```

## Arrays

Use the literal syntax for array creation. eslint: [`no-array-constructor`](http://eslint.org/docs/rules/no-array-constructor.html)

```javascript
// bad
const items = new Array()

// good
const items = []
```

Use [Array#push](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) instead of direct assignment to add items to an array.

```javascript
const someStack = []

// bad
someStack[someStack.length] = 'abracadabra'

// good
someStack.push('abracadabra')
```

Use array spreads `...` to copy arrays.

```javascript
// bad
const len = items.length
const itemsCopy = []
let i

for (i = 0 i < len i++) {
  itemsCopy[i] = items[i]
}

// good
const itemsCopy = [...items]
```

Use return statements in array method callbacks. It's ok to omit the return if the function body consists of a single statement following [8.2](#8.2). eslint: [`array-callback-return`](http://eslint.org/docs/rules/array-callback-return)

```javascript
// good
[1, 2, 3].map((x) => {
  const y = x + 1
  return x * y
})

// good
[1, 2, 3].map(x => x + 1)

// bad
const flat = {}
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item)
  flat[index] = flatten
})

// good
const flat = {}
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item)
  flat[index] = flatten
  return flatten
})

// bad
inbox.filter((msg) => {
  const { subject, author } = msg
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee'
  } else {
    return false
  }
})

// good
inbox.filter((msg) => {
  const { subject, author } = msg
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee'
  }

  return false
})
```

Use object destructuring when accessing and using multiple properties of an object. jscs: [`requireObjectDestructuring`](http://jscs.info/rule/requireObjectDestructuring)

> Why? Destructuring saves you from creating temporary references for those properties.

```javascript
// bad
function getFullName(user) {
  const firstName = user.firstName
  const lastName = user.lastName

  return `${firstName} ${lastName}`
}

// good
function getFullName(user) {
  const { firstName, lastName } = user
  return `${firstName} ${lastName}`
}

// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`
}
```

Use array destructuring. jscs: [`requireArrayDestructuring`](http://jscs.info/rule/requireArrayDestructuring)

```javascript
const arr = [1, 2, 3, 4]

// bad
const first = arr[0]
const second = arr[1]

// good
const [first, second] = arr
```

Use object destructuring for multiple return values, not array destructuring. jscs: [`disallowArrayDestructuringReturn`](http://jscs.info/rule/disallowArrayDestructuringReturn)

> Why? You can add new properties over time or change the order of things without breaking call sites.

```javascript
// bad
function processInput(input) {
  // then a miracle occurs
  return [left, right, top, bottom]
}

// the caller needs to think about the order of return data
const [left, __, top] = processInput(input)

// good
function processInput(input) {
  // then a miracle occurs
  return { left, right, top, bottom }
}

// the caller selects only the data they need
const { left, top } = processInput(input)
```
