```js
/**
 * @param {number} n
 * @return {boolean}
 */
var isHappy = function (n) {
  const nums = new Set();
  let current = n;
  while (true) {
    next = getNext(current);
    if (next === 1) {
      return true;
    }
    if (nums.has(next)) {
      return false;
    }
    nums.add(next);
    current = next;
  }
};

function getNext(num) {
  let next = 0;
  while (num > 0) {
    const modulo = num % 10;
    next += modulo ** 2;
    num = (num - modulo) / 10;
  }
  return next;
}
```
