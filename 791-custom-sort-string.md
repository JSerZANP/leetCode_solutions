
Here is my youtube video to explaing this : https://youtu.be/sgiAbThnatY


```js
/**
 * @param {string} S
 * @param {string} T
 * @return {string}
//  */
// var customSortString = function(S, T) {
//     // 1. get the Map<char, index>
//     // 2. create compare
//     // 3. use sort()
  
//     const orderMap = new Map()
//     for (let i = 0; i < S.length; i++) {
//       orderMap.set(S[i], i)
//     }
//     // O(nlogn)
//     const compare = (a, b) => {
//       if (!orderMap.has(a)) return -1
//       if (!orderMap.has(b)) return 1
//       return orderMap.get(a) - orderMap.get(b)
//     }
    
//     const chars = T.split('')
//     chars.sort(compare)
  
//     return chars.join('')
// };

var customSortString = function(S, T) {
    const count = new Map()
    for (let char of T) {
      if (count.has(char)) {
        count.set(char, count.get(char) + 1)
      } else {
        count.set(char, 1)
      }
    }
  
    let result = ''
    for (let char of S) {
      if (count.has(char)) {
        let num = count.get(char)
        while (num > 0) {
          result += char
          num -= 1
        }
        
        count.delete(char)
      }
    }
  
    for (let [char, num] of count) {
      while (num > 0) {
        result += char
        num -= 1
      }
    }
  
    return result
};
```
