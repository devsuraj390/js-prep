### Polyfills:

- https://javascript.info/polyfills

**promise.all():**

```js
Promise.myAll = function (promises) {
  return new Promise((resolve, reject) => {
    let results = [];
    let completed = 0;

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
