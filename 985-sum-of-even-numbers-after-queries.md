Here is a youtube video explaining this: https://youtu.be/LwZ0MZ7Z7sk

```js
/**
 * @param {number[]} A
 * @param {number[][]} queries
 * @return {number[]}
 */
var sumEvenAfterQueries = function(A, queries) {
    const result = []
    let sum = A.reduce((sum, item) => {
            return sum + (item % 2 === 0 ? item : 0)
        }, 0)
    
    
    for (let query of queries) {
        const prev = A[query[1]]
        const curr = A[query[1]] + query[0]
        
        let delta = 0
        
        if (prev % 2 === 0 && curr % 2 !== 0) {
            delta = - prev
        }
        
        if (prev % 2 === 0 && curr % 2 === 0) {
            delta = curr - prev
        }
        
        if (prev % 2 !== 0 && curr % 2 === 0) {
            delta = curr
        }
        
        sum += delta
        A[query[1]] = curr
        
        result.push(sum)
    }
    
    return result
};
```
