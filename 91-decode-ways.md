Here is a video explaining this: https://youtu.be/1MI6vT0lZ2k

```js
/**
 * @param {string} s
 * @return {number}
 */

// recursion
// Time: best O(n), worst f(n) = 2f(n - 1) => O(2^N)
// var numDecodings = function(s) {
    
//    const check = (count, start) => {
        
//         const char = s[start]
        
//         if (char === '0') {
//             return 0
//         }
        
//         if (start >= s.length - 1) {
//             return 1
//         }
       
//         switch (char) {
//             case '1':
//                 // 10
//                 if (s[start + 1] === '0') {
//                     return check(count, start + 2)
//                 } else {
//                     //1 or 1x
//                     return check(count, start + 1) + check(count, start + 2)
//                 }
//             case '2':
//                 // 20
//                 if (s[start + 1] === '0') {
//                     return check(count, start + 2)
//                 } else {
//                     // 27
//                     if (s[start + 1] > 6) {
//                         return check(count, start + 1)
//                     } else {
//                         // 2. or 2x
//                         return check(count, start + 1) + check(count, start +2)
//                     }
//                 }
//             default:
//                 return check(count, start + 1)
//         }
//    } 
   
//    return check(0, 0)
// };


// DP
var numDecodings = function(s) {
    
   // '22' + '2'
   // for extra '6', stadalone (uses f(n - 1)), or combined (affects f(n - 2))
    
   // f(n) = f(n - 1) + f(n - 2) (conditions required)
   // s[n] is 0. s[n- 1] is 1 or 2, f(n - 2). or 0
   // s[n] is 1 ~ 6 ,s[n-1] is 1 or 2 , f(n - 2) + f(n - 1)
    // s[n - 1] is 1, f(n - 2) + f(n - 1)
    //  f(n - 1)
    const result = Array(s.length + 2).fill(1)
    
    for (let i = 0; i < s.length; i++) {
        const index = i + 2
        const char = s[i]
        if (char === '0') {
            if (['1', '2'].includes(s[i - 1])) {
                result[index] = result[index - 2]
            } else {
                return 0
            }
        } else if ( char < 7) {
            if (['1', '2'].includes(s[i - 1])) {
                result[index] = result[index - 1] + result[index - 2]
            } else {
                result[index] = result[index - 1]
            }
        } else {
            if (s[i - 1] === '1') {
                result[index] = result[index - 1] + result[index - 2]
            } else {
                result[index] = result[index - 1]
            }
        }
    }
    
    return result[s.length - 1 + 2]
};
```
