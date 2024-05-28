```js
/**
 * @param {number[]} coins
 * @param {number} amount
 * @return {number}
 */
// O(C*A)
var coinChange = function (coins, amount) {
  const numOfCoins = new Array(amount + 1).fill(Infinity);
  numOfCoins[0] = 0;
  for (let i = 0; i < amount; i++) {
    for (const coin of coins) {
      numOfCoins[i + coin] = Math.min(numOfCoins[i + coin], numOfCoins[i] + 1);
    }
  }
  return numOfCoins[amount] === Infinity ? -1 : numOfCoins[amount];
};
```

Above is very slow though, can we do better?
