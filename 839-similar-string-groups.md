Here is me explaining this:  https://youtu.be/2PihCv4bD3A

```js
/**
 * @param {string[]} A
 * @return {number}
 */

// m words  at length n

// Time: O(m ^ 2 n)
// Space: O(m^2)
var numSimilarGroups = function(A) {
    // word1 <-> word2
    // word2 <-> word3
  
    // check all connected words
    // then try to count how many isolated subgraph
  
    // how to express a graph?
    // Map<word, Set<word>>
  
    // ['tars', ['rats', 'tras']]
    // ['rats', ['tars', ..]]
  
    // how to count isolated subgraph?
    // pick a node, DFS/BFS traverse the whole graph. (mark traversed node to prevent circles)
    // conitnue above process for all nodes 
  
    // how to check if two are similar
    // naively: O(n + n^2 + n) => O(n^2) 
    
    // or check by counding unmatching indexes 
    
    // O(n) O(1)
    const isSimilar = (word1, word2) => {
      let differentPositionCount = 0
      for (let i = 0; i < word1.length; i++) {
        if (word2[i] !== word1[i]) {
          differentPositionCount +=1
        }
        
        if (differentPositionCount > 2) {
          return false
        }
      }
      
      return differentPositionCount === 2
    }
    
    // O(m) O(m^2)
    const similarWordMap = new Map(A.map(word => [word, new Set()]))
    
    // O(m ^ 2 n)
    // fill up the map
    for (let i = 0; i < A.length - 1; i++) {
      for (let j = i + 1; j < A.length; j++) {
        if (isSimilar(A[i], A[j])) {
          similarWordMap.get(A[i]).add(A[j])
          similarWordMap.get(A[j]).add(A[i])
        }
      }
    }
  
  
    // O(m)
    // traverse through the graph and count isolated sub graph
    const traversed = new Set()
    let count = 0
    
    // O(m) O(m)
    for (let word of A) {
      if (traversed.has(word)) continue
      // if ok, then this is a new subgraph
      count += 1
      // mark all the connected nodes
      // DFS, stack
      // O(m)
      const stack = [word]
      while (stack.length > 0) {
        const top = stack.pop()
        traversed.add(top)
        
        // check its connect words
        for (let next of similarWordMap.get(top)) {
          if (!traversed.has(next)) {
            stack.push(next)
          }
        }
      }
    }
    
    return count
};














```
