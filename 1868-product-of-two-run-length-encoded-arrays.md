## 1. Naive approach following the description => Memory allocation error

```js
// N - the expanded length, K - the compressed length
var findRLEArray = function (encoded1, encoded2) {
  return compress(getProduct(expand(encoded1), expand(encoded2)));
};

// O(N), O(N)
function expand(encoded) {
  const result = [];
  for (let [num, freq] of encoded) {
    while (freq > 0) {
      result.push(num);
      freq -= 1;
    }
  }
  return result;
}

// O(N), O(K)
function compress(arr) {
  const result = [];
  let buffer = null;
  for (const item of arr) {
    if (buffer === null) {
      buffer = [item, 1];
    } else if (buffer[0] === item) {
      buffer[1] += 1;
    } else {
      result.push(buffer);
      buffer = [item, 1];
    }
  }
  result.push(buffer);
  return result;
}

// O(N), O(K)
function getProduct(arr1, arr2) {
  if (arr1.length !== arr2.length) {
    throw "lists should have same length";
  }
  return arr1.map((item, index) => item * arr2[index]);
}
```

## 2. Improved approach by getting product from the encoded directly.

1. need to push items back if length doesn't match
2. merge to the previous buffer if number is the same

TLE > `shift()` causes more than O(N) because we need to re-index the items

```js
// N - the expanded length, K - the compressed length
// O(K) ?, O(K)
var findRLEArray = function (encoded1, encoded2) {
  // [[1,3],[2,3]] x [[6,3],[3,3]]
  // [6, 3], [6, 3]
  // [6, 6]

  // [[1,3],[2,1],[3,2]] x [[2,3],[3,3]]
  // [2, 3], [6, 1]  [3,2] x[3, 2]
  // [2, 3], [6, 1], [9, 2]

  // try to get. product of first items
  // split the longer one
  // merge by comparing the item
  const result = [];
  let buffer = null;

  while (encoded1.length > 0) {
    const head1 = encoded1.shift();
    const head2 = encoded2.shift();

    const length = Math.min(head1[1], head2[1]);

    if (head1[1] > length) {
      encoded1.unshift([head1[0], head1[1] - length]);
      head1[1] = length;
    }

    if (head2[1] > length) {
      encoded2.unshift([head2[0], head2[1] - length]);
      head2[1] = length;
    }

    const product = [head1[0] * head2[0], head1[1]];
    if (buffer === null) {
      buffer = product;
    } else if (buffer[0] === product[0]) {
      buffer[1] += product[1];
    } else {
      result.push(buffer);
      buffer = product;
    }
  }

  result.push(buffer);

  return result;
};
```

## 3. Switching to `pop()`.

```js
var findRLEArray = function (encoded1, encoded2) {
  // [[1,3],[2,3]] x [[6,3],[3,3]]
  // [6, 3], [6, 3]
  // [6, 6]

  // [[1,3],[2,3]] x [[6,3],[3,3]]
  // [6, 3], [6, 3]
  // [6, 6]

  // [[1,3],[2,1],[3,2]] x [[2,3],[3,3]]
  // [9, 2], [6, 1], [2, 3]

  // try to get. product of first items
  // split the longer one
  // merge by comparing the item
  const result = [];
  let buffer = null;

  while (encoded1.length > 0) {
    const head1 = encoded1.pop();
    const head2 = encoded2.pop();

    const length = Math.min(head1[1], head2[1]);

    if (head1[1] > length) {
      encoded1.push([head1[0], head1[1] - length]);
      head1[1] = length;
    }

    if (head2[1] > length) {
      encoded2.push([head2[0], head2[1] - length]);
      head2[1] = length;
    }

    const product = [head1[0] * head2[0], head1[1]];
    if (buffer === null) {
      buffer = product;
    } else if (buffer[0] === product[0]) {
      buffer[1] += product[1];
    } else {
      result.push(buffer);
      buffer = product;
    }
  }

  result.push(buffer);
  result.reverse();
  return result;
};
```
