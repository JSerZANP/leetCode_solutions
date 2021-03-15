Here is my video explaining this: https://youtu.be/j2EV6sbYHnE

```js
/**
 * @param {number} n
 * @return {number}
 */
var countPrimes = function(n) {
    // to check if a number i is prime
    // divide i with all number [0, sqrt[i]]
    // O(n * sqrt(n))
  
    // 2: O
    // 4: x
    // 6: x
    // get a prime, and we could filter out a lot of non-prime numbers
  
    const isPrime = new Array(n).fill(true)
    isPrime[0] = false
    isPrime[1] = false
  
    for (let i = 2; i * i < n; i++) {
      if (!isPrime[i]) continue
      
      for (let j = i; i * j < n; j++) {
        isPrime[i * j] = false
      }
    }
  
    return isPrime.reduce((count, isPrime) => {
        if (isPrime) count += 1
        return count
    }, 0)
};
```
