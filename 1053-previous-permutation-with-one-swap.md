Me explaining this problem on youtube: https://youtu.be/yJGdxk5t3I8


```js
/**
 * @param {number[]} A
 * @return {number[]}
 */
var prevPermOpt1 = function(A) {
    const swap = (i, j) => {
        const temp = A[i]
        A[i] = A[j]
        A[j] = temp
    }
    
    // 1. from right to left,  find the first upward slope
    for (let i = A.length; i >= 0; i--) {
        if (A[i] < A[i - 1]) {
            // 2. from left to right, search for largest number which is not larger than the slope
            let target = i
            let j = i + 1
            while (A[j] < A[i - 1]) {
                if (A[j] !== A[j - 1]) {
                    target = j
                }
                j += 1
            }
            
            // 3. swap
            swap(i - 1, target)
            break
        }
    }
    
    return A
    
};
```
