## 1. brute force

```js
// O(h * n)
var hIndex = function (citations) {
  let h = 1;
  while (true) {
    if (citations.filter((citation) => citation >= h).length < h) {
      break;
    } else [(h += 1)];
  }
  return h - 1;
};
```

## 2. Binary Search

```js
// binary search
// O(logH * n)
var hIndex = function (citations) {
  let i = 0;
  let j = 1000;

  while (i <= j) {
    const m = Math.floor((i + j) / 2);
    if (isValid(m)) {
      i = m + 1;
    } else {
      j = m - 1;
    }
  }

  // when it ends
  // i is where h is invalid

  function isValid(h) {
    return citations.filter((citation) => citation >= h).length >= h;
  }

  return i - 1;
};
```

## 3. Sorting

```js
// if we sort it first
// [6, 5, 3, 1, 0]
// then we can just search and find 3 , decresing citation + increasing papaer count
// // O(nlogn)
var hIndex = function (citations) {
  citations.sort((a, b) => b - a);
  let h = 0;
  for (let i = 0; i < citations.length; i++) {
    if (citations[i] >= i + 1) {
      h = i + 1;
    }
  }
  return h;
};
```

## 4. counting

```js
var hIndex = function (citations) {
  const buckets = new Array(1001).fill(0);
  for (let i = 0; i < citations.length; i++) {
    buckets[citations[i]] += 1;
  }

  // count and compare
  let sum = 0;
  for (let i = buckets.length - 1; i >= 0; i--) {
    sum += buckets[i];
    // means for h of i, there are sum papers
    if (sum >= i) {
      return i;
    }
  }
  // search the maximum that has enough citations
};
```

## 5. Improved counting

```js
var hIndex = function (citations) {
  const n = citations.length;
  const l = Math.min(n, 1000);
  const buckets = new Array(l + 1).fill(0);
  for (let i = 0; i < citations.length; i++) {
    buckets[Math.min(citations[i], l)] += 1;
  }
  // count and compare
  let sum = 0;
  for (let i = buckets.length - 1; i >= 0; i--) {
    sum += buckets[i];
    // means for h of i, there are sum papers
    if (sum >= i) {
      return i;
    }
  }
  // search the maximum that has enough citations
};
```
