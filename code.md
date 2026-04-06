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
Array.prototype.myReduce = function (callbackFn, initialValue) {
  if (typeof callbackFn !== 'function') {
    throw new TypeError('callbackFn must be a function');
  }

  const noInitValue = initialValue === undefined;
  const length = this.length;

  if (noInitValue && length === 0) {
    throw new TypeError('Reduce of empty array with no initial value');
  }

  let acc = noInitValue ? this[0] : initialValue;
  let start = noInitValue ? 1 : 0;

  for (let i = start; i < length; i++) {
    if (Object.prototype.hasOwnProperty.call(this, i)) {
      acc = callbackFn(acc, this[i], i, this);
    }
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

**flatten an array:**

```js
// flatten([1, 2, 3, [4, 5], 6]) --> [1, 2, 3, 4, 5, 6]

// Approach 1: Using recursion
function flatten(arr) {
  let result = [];

  for (let item of arr) {
    if (Array.isArray(item)) {
      result = result.concat(flatten(item));
    } else {
      result.push(item);
    }
  }

  return result;
}

// Approach 2: Using reduce()
function flatten(arr) {
  return arr.reduce((acc, curr) => {
    if (Array.isArray(curr)) {
      return acc.concat(flatten(curr));
    }
    return acc.concat(curr);
  }, []);
}
```
