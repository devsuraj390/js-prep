### Polyfills:

- https://javascript.info/polyfills

**array.map():**

```js
Array.prototype.myMap = function (cb) {
  const result = [];

  for (let i = 0; i < this.length; i++) {
    result[i] = cb(this[i], i, this);
  }

  return result;
};
```

**array.reduce():**

```js
//Syntax
arr.reduce((accumulator, current, index, array) => {
  return updatedAccumulator;
}, initialValue);

//Polyfill
Array.prototype.myReduce = function (cb, acc) {
  let start = 0;

  if (acc === undefined) {
    acc = this[0];
    start = 1;
  }

  for (let i = start; i < this.length; i++) {
    acc = cb(acc, this[i], i, this);
  }

  return acc;
};
```

**promise.all():**

```js
Promise.myAll = function (promises) {
  return new Promise((resolve, reject) => {
    let results = [];
    let completed = 0; // To track how many promises have completed

    if (promises.length === 0) {
      return resolve([]);
    }

    promises.forEach((promise, index) => {
      Promise.resolve(promise)
        .then((value) => {
          results[index] = value;
          completed++;

          if (completed === promises.length) {
            resolve(results);
          }
        })
        .catch((err) => reject(err));
    });
  });
};

const p1 = Promise.resolve(1);
const p2 = Promise.resolve(2);
const p3 = Promise.resolve(3);

Promise.myPromiseAll([p1, p2, p3])
  .then((result) => console.log(result)) // [1, 2, 3]
  .catch((err) => console.log(err));
```

**promise.any():**
**promise.allSettled():**

---

### Design Patterns:

---

### Coding

**debounce, throttle:**

- https://www.youtube.com/watch?v=cjIswDCKgu0&t=155s
- https://css-tricks.com/debouncing-throttling-explained-examples/

```js
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
