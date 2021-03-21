Here is the video explaining: https://youtu.be/21MLoK0zZBs

```js
/**
 * @param {number} a
 * @param {number} b
 * @param {number} c
 * @return {number}
 */
var maximumScore = function(...args) {
    const [a, b, c] = args.sort((x, y) => y - x)
    
    if (b + c <= a) return b + c

    // 6 4 4   => empty 6 because 4 + 4 > 6, 
    // while empty 6, we could empty 4 or ther other 4, because 6 is the largest number
    // could balance the rest 2 piles while empty the largest pile
    // a, b, c
    // a >= b, a >= c, a >= b > b - c
    // empty a first 
    return a + Math.floor((b + c - a) / 2)

};
```
