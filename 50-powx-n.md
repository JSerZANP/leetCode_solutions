A video explaining this: https://youtu.be/ZWrYU-xnGLE

```js
/**
 * @param {number} x
 * @param {number} n
 * @return {number}
 */
// naive implemention  iterative TLE
// TIME: O(n)
// Space: O(1)
// var myPow = function(x, n) {
//     let result = 1

//     if (n < 0) {
//       x = 1 / x
//       n = -n
//     }

//     while (n-- > 0) {
//       result *= x
//     }
//     return result
// };

// Recursion
// TIME: O(n)
// non-tail: Space: O(n)  call stack siz exceeded
// var myPow = function(x, n) {
//     if (n === 0) {
//       return 1
//     }

//     if (n < 0) {
//       x = 1 / x
//       n = -n
//     }

//     return myPow(x, n - 1) * x
// };

// x**11 = (x**5) ** 2 * x
// improved recursion
// non-tail
// TIME: O(log(n))
// Space: O(log(n)) on-tail
var myPow = function (x, n) {
  if (n === 0) {
    return 1;
  }

  if (n === 1) {
    return x;
  }

  if (n < 0) {
    x = 1 / x;
    n = -n;
  }

  if (n % 2 === 1) {
    return myPow(x, (n - 1) / 2) ** 2 * x;
  } else {
    return myPow(x, n / 2) ** 2;
  }
};

// improved iteration
// 13 -> 1101  =  2**3 + 2**2 + 2**0
// x**(2**3) * (x ** (2**2)) * (x ** (2 ** 0))
// in binary format
// bases: 2**3      2**2      2**1     2**0
// what we need is to collect the digit where bit is 1
var myPow = function (x, n) {
  if (n === 0) {
    return 1;
  }

  if (n < 0) {
    x = 1 / x;
    n = -n;
  }

  let result = 1;
  let base = x ** (2 ** 0);

  while (n > 1) {
    if (n % 2 === 1) {
      result *= base;
      n = (n - 1) / 2;
    } else {
      n = n / 2;
    }
    base *= base;
  }

  result *= base;
  return result;
};
```

```js
/**
 * @param {number} x
 * @param {number} n
 * @return {number}
 */
// O(logn), O(logn)
// var myPow = function(x, n) {
//     if (n === 0) return 1
//     if (n < 0) return 1 / myPow(x, -n)
//     if (n === 1) return x
//     if (n % 2 === 0) {
//         const half = myPow(x, n / 2)
//         return half * half
//     } else {
//         const half = myPow(x, (n - 1) / 2)
//         return half * half * x
//     }
// };

// iterative
var myPow = function (x, n) {
  if (n === 0) return 1;
  let sign = 1;
  if (n < 0) {
    sign = -1;
    n = -n;
  }

  // x ^ n = (x ^ 2) ^ ( n / 2)

  let result = 1;
  while (n > 1) {
    if (n % 2 === 1) {
      result *= x;
      n = n - 1;
    }
    n = n / 2;
    x = x * x;
  }
  result = result * x;
  if (sign < 0) return 1 / result;
  return result;
};

// 2, 10 1
// 2 ^ 2, 5, 1
// 2 ^ 4, 2, 2 ^ 2
// 2 ^ 8, 1, 2 ^ 2
//
```
