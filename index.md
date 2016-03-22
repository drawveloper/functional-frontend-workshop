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
- Function composition
- Immutability

--

> “The problem with object-oriented languages is they’ve got all this implicit environment that they carry around with them. You wanted a banana but what you got was a gorilla holding the banana and the entire jungle.”  
~ Joe Armstrong

--

### Simple

`sim-plex` - "One fold/braid"  

> The opposite of this word is complex, which means braided together or folded together.  
> What matters for simplicity is that there is no interleaving.

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

> Pure functions bound the cognitive load of programming. When you’re writing a pure function, you only need to concern yourself with the body of the function. You don’t need to worry about externalities that could cause problems

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

# Thanks!

## 💥💥💥

--

http://www.infoq.com/presentations/Simple-Made-Easy
https://medium.com/@chetcorcos/functional-programming-for-javascript-people-1915d8775504#.cua401bvt
https://medium.com/javascript-scene/the-two-pillars-of-javascript-pt-2-functional-programming-a63aa53a41a4#.e0mu1pf8a
https://danmartensen.svbtle.com/javascripts-map-reduce-and-filter
