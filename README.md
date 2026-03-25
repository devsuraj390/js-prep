# js-prep

This repository includes a list of JavaScript topics along with related articles and blog references.

---

#### ✅ 1. Foundations

**'strict' mode:**

- https://www.geeksforgeeks.org/use-strict-in-javascript/
- https://medium.com/@catherineisonline/what-is-strict-mode-in-javascript-75929adbe844

**Scope and Hoisting:**

- https://dmitripavlutin.com/javascript-hoisting-in-details/
- https://medium.com/@AlexanderObregon/javascript-scope-and-hoisting-explained-dec184eb94b8

**var, let & const:**

- https://blog.webdevsimplified.com/2020-01/var-vs-let-vs-const/

**Arrow Functions:**

- https://dmitripavlutin.com/javascript-arrow-functions/
- https://javascript.info/arrow-functions-basics
- https://www.youtube.com/watch?v=6sQDTgOqh-I

**rest, spread operator:**

- https://javascript.info/rest-parameters-spread

**type conversions:**

- https://javascript.info/type-conversions

**nullish-coalescing operator:**

- https://javascript.info/nullish-coalescing-operator

#### ✅ 2. Core Engine

**Execution Context and Scope Chain:**

- https://dev.to/jahid6597/javascript-execution-context-a-deep-dive-4kno
- https://www.freecodecamp.org/news/how-javascript-works-behind-the-scene-javascript-execution-context/

**'this' keyword:**

- https://www.youtube.com/watch?v=YOlr79NaAtQ
- https://medium.com/codex/understanding-this-in-javascript-the-complete-guide-c4c21fe15ff8
- https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/

**call, apply and bind:**

- https://medium.com/@omergoldberg/javascript-call-apply-and-bind-e5c27301f7bb
- https://www.geekster.in/articles/call-apply-bind-methods-in-javascript/

**closure:**

- https://javascript.info/closure
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Closures

**prototype, inheritance:**

- https://javascript.info/prototypes

### ✅ 3. Async JS

**Callbacks:**

- https://javascript.info/callbacks

**Event Loop:**

- https://javascript.info/event-loop
- https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Execution_model
- https://developer.mozilla.org/en-US/docs/Web/API/Window/setTimeout

**microtasks / macrotasks:**

- https://javascript.info/event-loop#macrotasks-and-microtasks

**Promise:**

- https://javascript.info/promise-basics
- https://javascript.info/promise-chaining
- https://javascript.info/promise-error-handling
- https://javascript.info/promise-error-handling
- https://blog.webdevsimplified.com/2021-09/javascript-promises/
- https://javascript.info/promise-api

**error handling:**

- https://javascript.info/error-handling

**setTimeout, setInterval:**

- https://javascript.info/settimeout-setinterval

#### ✅ 4. Objects, Copying and Functional Patterns

**Shallow Copy and Deep Copy:**

- https://medium.com/version-1/cloning-an-object-in-javascript-shallow-copy-vs-deep-copy-fa8acd6681e9

**currying:**

- https://javascript.info/currying-partials

**piping:**

**method-chaining:**

#### ✅ 5. Browser APIs

**'load' and 'DOMContentLoaded' event:**

- https://www.geeksforgeeks.org/difference-between-domcontentloaded-and-load-events/
- https://javascript.info/onload-ondomcontentloaded

**async v/s defer:**

- https://blog.webdevsimplified.com/2019-12/javascript-loading-attributes-explained/
- https://javascript.info/script-async-defer

**Event Propagation, Bubbling, Capturing:**

- https://dev.to/anshumanmahato/managing-event-flow-a-deep-dive-into-javascript-event-propagation-2gha
- https://javascript.info/bubbling-and-capturing

**Event Delegation:**

- https://www.freecodecamp.org/news/event-delegation-javascript/
- https://javascript.info/event-delegation
- https://dev.to/shafayeat/mastering-javascript-event-delegation-3k2k

**localStorage, sessionStorage and cookies:**

- https://javascript.info/data-storage
- https://www.xenonstack.com/insights/local-vs-session-storage-cookie
- https://www.geeksforgeeks.org/difference-between-local-storage-session-storage-and-cookies/
- https://stackoverflow.com/questions/19867599/what-is-the-difference-between-localstorage-sessionstorage-session-and-cookies

**mutation observers:**

- https://javascript.info/mutation-observer

#### ✅ 6. Advanced

**modules:**

- http://javascript.info/modules

**generators, iterators:**

- https://javascript.info/generators-iterators

**memory management & garbage collection:**

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Memory_management

---

### Polyfills:

- https://javascript.info/polyfills

**promise.all():**

---

### Design Patterns:

---

### Coding

**debounce, throttle:**

- https://www.youtube.com/watch?v=cjIswDCKgu0&t=155s
- https://css-tricks.com/debouncing-throttling-explained-examples/

```
function debounce(cb, delay) {
    let timeout;

    return (...args) => {
        clearTimeout(timeout);
        timeout = setTimeout(() => {
            cb(...args);
        }, delay)
    }
}

// To call
const debounced = debounce(text => {
    ...
}, 1000)

```

---

### DSA

**arrays:**

- https://javascript.info/array

**objects:**

- https://javascript.info/object-basics

**linked-list:**

**trees:**

**hashmap:**

**hashset:**

**searching:**

**sorting:**

---

#### References:

- https://javascript.info/
- https://developer.mozilla.org/en-US/
- https://www.youtube.com/@WebDevSimplified
- https://alpha.learnersbucket.com/
