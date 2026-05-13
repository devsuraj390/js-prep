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

**array.filter():**

```js
Array.prototype.myFilter = function (callback) {
  const result = [];

  for (let i = 0; i < this.length; i++) {
    if (callback(this[i], i, this)) {
      result.push(this[i]);
    }
  }

  return result;
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

```js
function promiseAllSettled(promises) {
  return new Promise((resolve) => {
    if (promises.length === 0) {
      return resolve([]);
    }

    const results = [];
    let completed = 0;

    promises.forEach((promise, index) => {
      Promise.resolve(promise)
        .then((value) => {
          results[index] = {
            status: 'fulfilled',
            value: value,
          };
        })
        .catch((error) => {
          results[index] = {
            status: 'rejected',
            reason: error,
          };
        })
        .finally(() => {
          completed++;

          if (completed === promises.length) {
            resolve(results);
          }
        });
    });
  });
}
```

**call, apply, bind:**

```js
// call
Function.prototype.myCall = function (context, ...args) {
  return this.apply(context, args);
};

// -> Without using apply:
Function.prototype.myCall = function (context, ...args) {
  context.fn = this;

  const result = context.fn(...args);

  delete context.fn;

  return result;
};

// apply

// bind
Function.prototype.myBind = function (context, ...presetArgs) {
  const fn = this;

  return function (...laterArgs) {
    return fn.apply(context, [...presetArgs, ...laterArgs]);
  };
};
```

---

### Design Patterns:

---

### Coding

**Deep Copy in Objects:**

```js
function deepClone(obj) {
  if (obj === null || typeof obj !== 'object') return obj;

  let copy = Array.isArray(obj) ? [] : {};

  for (let key in obj) {
    copy[key] = deepClone(obj[key]);
  }

  return copy;
}
```

**debounce, throttle:**

- https://www.youtube.com/watch?v=cjIswDCKgu0&t=155s
- https://css-tricks.com/debouncing-throttling-explained-examples/

```js
function debounce(fn, delay) {
    let timeout;

    return function(...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => {
            fn.apply(this, args)
        }, delay)
    }
}

// To call
const debounced = debounce(text => {
    ...
}, 1000)

//Throttle
function throttle(fn, delay) {
  let lastCallTime = 0;

  return function (...args) {
    const now = Date.now();

    if(now - lastCallTime >= delay) {
      lastCallTime = now;
      fn.apply(this, args);
    }
  }
}

//To call
const throttled = throttle(fn, delay);
throttled(); ✅ runs immediately
throttled(); ❌ ignored
throttled(); ❌ ignored

// after 1 sec
throttled(); ✅ runs again

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

**flatten an object:**

```js
Input: flattenObject({
  user: {
    name: 'Suraj',
    address: {
      city: 'Hyderabad',
    },
  },
});

//Output:
{
  "user.name": "Suraj",
  "user.address.city": "Hyderabad"
}

function flattenObject(obj) {
  const result = {};

  function helper(currentObj, parentKey) {
    for (let key in currentObj) {
      if (currentObj.hasOwnProperty(key)) {
        const newKey = parentKey ? `${parentKey}.${key}` : key;

        if (
          typeof currentObj[key] === "object" &&
          currentObj[key] !== null &&
          !Array.isArray(currentObj[key])
        ) {
          helper(currentObj[key], newKey);
        } else {
          result[newKey] = currentObj[key];
        }
      }
    }
  }

  helper(obj, "");

  return result;
}
```

**Memoize Fn:**

```js
function memoize(fn) {
  const cache = {};

  return function (...args) {
    const key = JSON.stringify(args);

    if (cache[key]) {
      return cache[key];
    }

    const result = fn.apply(this, args);
    cache[key] = result;
    return result;
  };
}
```

**Event Delegation:**

```html
<ul id="list">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

Implement click handling such that:

- Clicking any `<li>` logs its text.
- Only one event listener is used.

```js
const list = document.getElementById('list');
list.addEventListener('click', (e) => {
  const li = e.target.closest('li');

  if (li & list.contains(li)) {
    console.log(li.textContent);
  }
});
```

**LRU Cache:**

```js

```

#### JS Coding

```js
//Input
const data = [
  { country: 'IN', state: 'TN', outlets: 4 },
  { country: 'US', state: 'CA', outlets: 2 },
  { country: 'IN', state: 'AP', outlets: 8 },
  { country: 'US', state: 'LA', outlets: 3 },
  { country: 'UK', state: 'SD', outlets: 9 },

  //Output
  [
    { country: 'IN', stateCount: 2, totalOutlets: 12 },
    { country: 'US', stateCount: 2, totalOutlets: 5 },
    { country: 'UK', state: 'SD', outlets: 9 },
  ],
];

// Solution
const grouped = {};

data.forEach((item) => {
  const { country, state, outlets } = item;

  if (!grouped[country]) {
    grouped[country] = {
      states: new Set(),
      totalOutlets: 0,
    };
  }

  grouped[country].states.add(state);
  grouped[country].totalOutlets += outlets;
});

const result = Object.keys(grouped).map((country) => {
  return {
    country,
    stateCount: grouped[country].states.size,
    totalOutlets: grouped[country].totalOutlets,
  };
});

console.log(result);
```

**Move zeros to end of array:**

```js
// Input - arr = [0, 1, 0, 3, 12, 0, 5];
// Output - [1, 3, 12, 5, 0, 0,  0]

// Note: Do changes in place and maintain order while moving zeros to the end
// The solution uses two pointers approach
function moveZerosToEnd(arr) {
  let insertPos = 0;

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] !== 0) {
      arr[insertPos] = arr[i];
      insertPos++;
    }
  }
  for (let i = insertPos; i < arr.length; i++) {
    arr[i] = 0;
  }
  return arr;
}

// Note: Instead of two loops, we can swap as well.
for (let i = 0; i < arr.length; i++) {
  if (arr[i] !== 0) {
    [arr[i], arr[insertPos]] = [arr[insertPos], arr[i]];
    insertPos++;
  }
}
```

**Maximum Sum Subarray of Size K:**

```js
// Sliding Window Pattern
const nums = [2, 1, 5, 1, 3, 2];
const size = 3;
Output: 9;
// Pattern: newWindow = oldWindow + incoming - outgoing
```

<details>
<summary>See Solution</summary>

```js
function maxSubArraySum(arr, size) {
  let maxSum = 0;

  // Step 1: initial window
  for (let i = 0; i < size; i++) {
    maxSum += arr[i];
  }

  let tempSum = maxSum;

  // Step 2: slide the window
  for (let i = size; i < arr.length; i++) {
    tempSum = tempSum + arr[i] - arr[i - size];
    maxSum = Math.max(maxSum, tempSum);
  }

  return maxSum;
}
```

</details>
