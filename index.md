title: Functional Frontend
output: index.html
style: style.css
author:
  name: Guilherme Rodrigues
  twitter: first_doit
  url: http://firstdoit.com

--

# Functional Frontend
## Useful Functional Paradigms in Frontend Development

--

### Contents

- "Simplicity"
- Pure functions
- `map` and `reduce`
- `const` vs `let`
- Immutability

--

### Simple

`sim-plex` - "One fold/braid"  

> The opposite of this word is complex, which means braided together or folded together.  
> What matters for simplicity is that there is no interleaving.

--

> “The problem with object-oriented languages is they’ve got all this implicit environment that they carry around with them. You wanted a banana but what you got was a gorilla holding the banana and the entire jungle.”  
~ Joe Armstrong

--

## The Functional Programming ideal

You can't get *simpler* than **Data and Functions**

--

### Pure functions

Pure functions are **idempotent** functions **without side effects** and **without external dependencies**.

```js
const pure = (a) => a + 1
const foo = 1
const bar = pure(foo)
console.log(foo, bar) // 1, 2
```

--

> Pure functions depend only on the inputs of the function, and the output should be the exact same for the same input.

--

### Impure by side effect

```js
let foo = 1
let sideEffect = () => foo = 2
sideEffect()
console.log(foo) // 2
```

--

### Impure by external dependency

```js
let foo = 1
let externalDep = (a) => foo + a
let qux = externalDep(2)
console.log(qux) // 3

foo = 3
qux = externalDep(2)
console.log(qux) // 5
```

--

> Pure functions bound the cognitive load of programming. When you’re writing a pure function, you only need to concern yourself with the body of the function. You don’t need to worry about externalities that could cause problems.

--

### Functional building blocks

- `map: (list) -> list`
- `reduce: (list) -> value`

--

### Array.prototype.map()

> The map() method creates a new array with the results of calling a provided function on every element in this array.

--

```js
[0, 1, 2, 3, 4].map(
  (value, currentIndex, array) => {
    return value + 1
  }
) // [1, 2, 3, 4, 5]
```

--

```js
const numbers = [1, 4, 9]
const roots = numbers.map(Math.sqrt)
// roots is now [1, 2, 3], numbers is still [1, 4, 9]
```

--

```js
const map = Array.prototype.map
const a = map.call('Hello World', (x) => x.charCodeAt(0))
// a now equals [72, 101, 108, 108, 111, ...]
```

--

### Array.prototype.reduce()

> The reduce() method applies a function against an accumulator and each value of the array (from left-to-right) to reduce it to a single value.

--

```js
[0, 1, 2, 3, 4].reduce(
  (previousValue, currentValue, currentIndex, array) => {
    return previousValue + currentValue
  }
) // 10
```

--

```js
[0, 1, 2, 3, 4].reduce( (prev, curr) => prev + curr ) // 10
```

--

```js
const sum = (prev, curr) => prev + curr
[0, 1, 2, 3, 4].reduce(sum, 10) // 20
```

--

### Functional utils

- `reverse() ([1, 2, 3]) -> [3, 2, 1]`
- `find() ([x]) -> x`
- `filter() ([x]) -> [y]`
- `any() — true if any values match predicate`
- `all() — true if all values match predicate`
- `sum() — total of all values`
- `product() — product of all values`
- `maximum() — highest value`
- `minimum() — lowest value`


--

They can all be written in terms of `map` and `reduce`

```js
r = (v, i, array) => array[array.length - 1 - i]
reverse = (a) => Array.prototype.map.call(a, r)
reverse([1, 2, 3]) // [3, 2, 1]
reverse('oba') // ["a", "b", "o"]
```

--

### `const` vs `let`

TL;DR: Always use `const`

> The const declaration creates a read-only reference to a value.

- `const`: "Great, this will stay the same"*
- `let`: "Uh-oh, need to keep this in mind"

\* doesn't mean immutable.

--

### Temporal Coupling

> A common problem in API design is temporal coupling, which occurs when there's an implicit relationship between two, or more, members of a class requiring clients to invoke one member before the other. This tightly couples the members in the temporal dimension.

--

Fails:

```java
var b = new EndpointAddressBuilder();
var e = b.ToEndpointAddress();
```

Succeeds:

```java
var b = new EndpointAddressBuilder();
b.Uri = new UriBuilder().Uri;
var e = b.ToEndpointAddress();
```

--

We already know side effects are not cool.  
How we discourage something not cool?  
We forbid it. 😂

> Much of what makes application development difficult is tracking mutation and maintaining state. Developing with immutable data encourages you to think differently about how data flows through your application.

--

### Immutability

> Immutable data cannot be changed once created, leading to much simpler application development, no defensive copying, and enabling advanced memoization and change detection techniques with simple logic.

--

### Memowat?

> In computing, memoization is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again.

(`shouldComponentUpdate?`)

--

```js
var map1 = Immutable.Map({a:1, b:2, c:3});
var map2 = map1.set('b', 2);
assert(map1.equals(map2) === true);
var map3 = map1.set('b', 50);
assert(map1.equals(map3) === false);
```

--

> The difference for the immutable collections is that methods which would mutate the collection, like push, set, unshift or splice instead return a new immutable collection. Methods which return new arrays like slice or concat instead return new immutable collections.

--

```js
var list1 = Immutable.List.of(1, 2);
var list2 = list1.push(3, 4, 5);
var list3 = list2.unshift(0);
var list4 = list1.concat(list2, list3);
assert(list1.size === 2);
assert(list2.size === 5);
assert(list3.size === 6);
assert(list4.size === 13);
assert(list4.get(0) === 1);
```

--

There and back again

```js
var deep = Immutable.Map({
  a: 1, b: 2, c: Immutable.List.of(3, 4, 5)
});
deep.toObject() // { a: 1, b: 2, c: List [ 3, 4, 5 ] }
deep.toArray() // [ 1, 2, List [ 3, 4, 5 ] ]
deep.toJS() // { a: 1, b: 2, c: [ 3, 4, 5 ] }
JSON.stringify(deep) // '{"a":1,"b":2,"c":[3,4,5]}'
```

--

### Why is any of this useful?

Procedural thinking encourages you to **create state** and **mutate** it.

Functional tools makes you think about **data** and **operations** on it.

--

```js
let words = content.split(/[\s.,\/:\n]+/);
let tally = {};
for (let i = 0; i < words.length; i++) {
  let word = words[i].toLowerCase();
  tally[word] = (tally[word] || 0) + 1;
}
```

--

```js
const words = content.split(/[\s.,\/:\n]+/);
const tally = words
  .map(function(str) {
    return str.toLowerCase()
  })
  .reduce(function(tally, word) {
    tally[word] = (tally[word] || 0) + 1;
    return tally;
  }, {})
```

--

```js
// operations
const lower = (str) => str.toLowerCase()
const tallyUp = (tally, word) => {
  tally[word] = (tally[word] || 0) + 1;
  return tally;
}
// data
const words = content.split(/[\s.,\/:\n]+/);
const tally = words
  .map(lower)
  .reduce(tallyUp, {})
```

--

### FP untangles operations from data

Operations become:

- Simpler
- Reusable
- Easier to change
- Easier to understand

--

For next time:

- `apply`, `call`, `bind`
- Composition
- Currying
- Ramda?

--

# Thanks!

## 💥💥💥

--

http://www.infoq.com/presentations/Simple-Made-Easy  
https://medium.com/@chetcorcos/functional-programming-for-javascript-people-1915d8775504#.cua401bvt  
https://medium.com/javascript-scene/the-two-pillars-of-javascript-pt-2-functional-programming-a63aa53a41a4#.e0mu1pf8a  
https://danmartensen.svbtle.com/javascripts-map-reduce-and-filter  
http://tobyho.com/2015/11/09/functional-programming-by-example/  
http://fr.umio.us/why-ramda/  
http://ramdajs.com  
http://blog.ploeh.dk/2011/05/24/DesignSmellTemporalCoupling/  
