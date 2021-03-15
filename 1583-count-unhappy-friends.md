here is a video explaining this : https://youtu.be/aUQbwFQQa0U
```js
/**
 * @param {number} n
 * @param {number[][]} preferences
 * @param {number[][]} pairs
 * @return {number}
 */
var unhappyFriends = function(n, preferences, pairs) {
    // [0, 1], [2,3]
    // 1 -> 3, 1 -> 2
    // Map<number, Set<number>>
    // 1 -> 3
    let unhappyFriends = new Set()
    const unhappyMap = new Map()
    
    for (let [a, b] of pairs) {
      for (let target of preferences[a]) {
        if (target === b) break
        
        // check if target -> b exist
        if (unhappyMap.has(target) && unhappyMap.get(target).has(a)) {
          unhappyFriends.add(target)
          unhappyFriends.add(a)
        }
        
        if (unhappyMap.has(a)){
          unhappyMap.get(a).add(target)
        } else {
          unhappyMap.set(a, new Set([target]))
        }
      }
      
      for (let target of preferences[b]) {
        if (target === a) break
         // check if target -> b exist
        if (unhappyMap.has(target) && unhappyMap.get(target).has(b)) {
          unhappyFriends.add(target)
          unhappyFriends.add(b)
        }
        if (unhappyMap.has(b)){
          unhappyMap.get(b).add(target)
        } else {
          unhappyMap.set(b, new Set([target]))
        }
      }
    }
  
    return unhappyFriends.size
};
```
