A video explaining this: https://youtu.be/LQXcCbTOE_c

```js
/**
 * @param {number} n
 * @param {number} k
 * @return {string}
 */

// Back Tracking (Naive)
// Time: O(k)??
// Space: O(n)?
// var getPermutation = function(n, k) {
//     let result
//     let count = 0

//     const walk = (temp, rest) => {
//       if (rest.length === 0) {
//         count += 1

//         if (count === k) {
//           result = temp.join('')
//           return 1
//         }
//       }

//       for (let i = 0; i < rest.length; i++) {
//         const newRest = rest.slice(0)
//         newRest.splice(i, 1)
//         const resultWalk = walk(temp.concat(rest[i]), newRest)
//         if (resultWalk) {
//           return 1
//         }
//       }

//       return 0
//     }

//     // generate the nums
//     // O(n)
//     const nums = []
//     while (n >= 1) {
//       nums.unshift(n);
//       n -= 1
//     }

//     walk([], nums)

//     return result
// };

// improve by avoding unncessarry generating
// jump the steps

// decide each digit from left to right

// Time: O(n)
// Space: O(n)
var getPermutation = function (n, k) {
  // firt , get the fac array
  const fac = [1, 1, 2];
  for (let i = 3; i <= n; i++) {
    fac.push(fac[i - 1] * i);
  }
  // means there would be fac[n] possibilities for n-digit

  // get all the digits
  // O(n)
  const nums = [];
  while (n >= 1) {
    nums.unshift(n);
    n -= 1;
  }

  const result = [];

  // what is the first digit of k-th possiblity?
  // for each didgit, there would be fac[n - 1] possibility

  // considering k = 1, and n = 2
  // it should be ceil - 1
  // <=1 => 0
  // 1 <= 2 => 1
  // O(n)
  while (nums.length > 0) {
    // get the first digit
    const index = Math.ceil(k / fac[nums.length - 1]) - 1;
    // update k by removing the possibilities
    k -= index * fac[nums.length - 1];

    result.push(nums[index]);
    nums.splice(index, 1);
  }

  return result.join("");
};
```

Another try in 2024

```js
/**
 * @param {number} n
 * @param {number} k
 * @return {string}
 */
var getPermutation = function (n, k) {
  // fix index i from left
  // there are (n - 1 - i)! permuations
  // so if n = 3

  // - - O => o! => 1
  // - O  => 1! = 1
  // O => 2! => 2

  // for n = 3
  // since for the first digt, there are 2 variations
  // so the first digit 2
  // then we find the 1st varation when first digit is 2
  // it become a similar problem of getPermuation of [1, 3] at 1

  // init a range [1, 2, 3, .... n]
  // also calculate the permuation of (n - 1 - i)!
  //              [(n - 1)! ..... 1]

  // recursively compare the first count vs k
  // and decide the digit and mark the digit is by set it to -1

  const range = getRange(1, n);
  const permutation = getPermuation(n);
  let result = "";

  for (let i = 0; i < n; i++) {
    if (k === 0) {
      // it means we need to get the reverse
      for (let j = n - 1; j > -1; j--) {
        if (range[j] !== -1) {
          result += range[j];
        }
      }
      break;
    }
    // for each index
    let candidateDigitIndex = Math.floor(k / permutation[n - 1 - i]) - 1;
    // this index means we can drop all its variations
    const digitIndex = Math.max(
      k % permutation[n - 1 - i] === 0
        ? candidateDigitIndex
        : candidateDigitIndex + 1,
      0
    );
    const j = findKthValidIndex(range, digitIndex);
    result += range[j];
    range[j] = -1;
    k = k % permutation[n - 1 - i];
  }

  return result;
};

function getRange(from, to) {
  const result = [];
  while (from <= to) {
    result.push(from);
    from += 1;
  }
  return result;
}

function getPermuation(n) {
  const result = [1];
  for (let i = 1; i <= n; i++) {
    result.push(result.at(-1) * i);
  }
  return result;
}

function findKthValidIndex(range, k) {
  let i = 0;
  let j = 0;
  while (j < range.length) {
    if (range[j] !== -1) {
      if (i === k) {
        return j;
      }

      i += 1;
    }
    j += 1;
  }
}
```
