A video explaining this: https://youtu.be/Tna92fSOQTs

```js
/**
 * @param {number} n
 * @return {string[]}
 */

/*

1. ()

2. ()()   (())

3 =  1 + 2
  =  2 + 1
  =  3 + 0
*/

// Recursion
// Time: f(n) = f(n - 1)* f(0) + f(n -2) * f(1) + f(n-3) * f(2) ?
// var generateParenthesis = function(n) {
//     if (n === 0) {
//       return ['']
//     }

//     if (n === 1) {
//       return ['()']
//     }

//     const result = []
//     for (let i = 1; i <= n; i++) {
//       const leftInner = generateParenthesis(i - 1)
//       const right = generateParenthesis(n - i)

//       leftInner.forEach(itemLeft => {
//         right.forEach(itemRight => {
//           result.push(`(${itemLeft})${itemRight}`)
//         })
//       })
//     }

//     return result
// };

// Iteration
var generateParenthesis = function (n) {
  const results = [[""], ["()"]];

  for (let i = 2; i <= n; i++) {
    const result = [];
    for (let j = 1; j <= i; j++) {
      const leftInner = results[j - 1];
      const right = results[i - j];
      leftInner.forEach((itemLeft) => {
        right.forEach((itemRight) => {
          result.push(`(${itemLeft})${itemRight}`);
        });
      });
    }
    results[i] = result;
  }

  return results[n];
};
```

Another try in 2024

```js
/**
 * @param {number} n
 * @return {string[]}
 */
var generateParenthesis = function (n) {
  // as long as the count of unmatched left parentheses is not negative then it is fine
  // in each move we can choose any parenthes either '(' or ')'
  const result = [];
  const place = (i, temp = [], stack = []) => {
    if (i === 2 * n + 1 || stack > n) {
      if (stack.length === 0) {
        result.push(temp.join(""));
      }
      return;
    }
    ["(", ")"].forEach((char) => {
      if (char === "(") {
        temp.push(char);
        stack.push(char);
        place(i + 1, temp, stack);
        stack.pop();
        temp.pop();
      } else {
        temp.push(char);
        const newStack = [...stack];
        if (newStack.at(-1) === "(") {
          newStack.pop();
          place(i + 1, temp, newStack);
        }
        temp.pop();
      }
    });
  };
  place(1);
  return result;
};
```
