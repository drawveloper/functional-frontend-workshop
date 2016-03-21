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

- Pure functions
- `map` and `reduce`
- `const` vs `let`
- "Simplicity"
- Function composition

--

### Pure functions

Pure functions are functions **without side effects** and **without external dependencies**.

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

--

# Thanks!

## 💥💥💥

--

https://medium.com/@chetcorcos/functional-programming-for-javascript-people-1915d8775504#.cua401bvt
