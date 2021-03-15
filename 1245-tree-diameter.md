watch my video of explanation: https://youtu.be/sLEaLSA4KOg

```js
/**
 * @param {number[][]} edges
 * @return {number}
 */

// recursion

// Time: O(n)
// Space: O(n)
var treeDiameter = function(edges) {
    // process the input first
    const children = []
    
    for (let [from, to] of edges) {
       if (!children[from]) children[from] = []
        children[from].push(to)
    }
    
    // return [diameter, height]
    const walk = (index) => {
        if (children[index] === undefined) return [0, 1]
        
        // loop through children to find
        // 1. max dimater
        // 2. top 2 heights
        
        let maxDiameter = 0
        let top2Heights = [0, 0] // desc
        
        for (let childIndex of children[index]) {
            const [diameter, height] = walk(childIndex)
            maxDiameter = Math.max(diameter, maxDiameter)
            
            if (height >= top2Heights[0]) {
                top2Heights[1] = top2Heights[0]
                top2Heights[0] = height
            } else if (height > top2Heights[1]) {
                top2Heights[1] = height
            }
        }
        
        return [
            Math.max(maxDiameter, top2Heights[0] + top2Heights[1]),
            Math.max(...top2Heights) + 1
        ]
    }
    
    return walk(0)[0]
    
};
```
