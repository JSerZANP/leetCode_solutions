Here is a video explaining it: https://youtu.be/2tRXbn3sGHc

```js
/**
 * @param {number[][]} graph
 * @return {boolean}
 */


// Time: n -> count of edges => O(n)
// Sapce: m - node length => O(m) + O(m) => O(m)
// Recursion to mark all the nodes
// var isBipartite = function(graph) {
  
//     // 0 -- unnset
//     // 1 -- set A
//     // 2 -- set B
//     const marks = new Array(graph.length).fill(0)
    
//     const walk = (node, mark) =>  {
//       // it is already traversed
//       if (marks[node] !== 0) {
//         if (marks[node] !== mark) {
//           return false
//         }
//       } else {
//         marks[node] = mark
        
//         // recursively mark the adjascent nodes
//         const nextMark = mark === 1 ? 2: 1
        
//         for (let nextNode of graph[node]) {
//           if (!walk(nextNode, nextMark)) {
//             return false
//           }
//         }
//       }
//       return true
//     }
    
//     for (let i = 0; i < graph.length; i++) {
//       if (marks[i] === 0) {
//         if (!walk(i, 1)) return false
//       }
//     }
  
//     return true
// };

//DFS with a stack
// Time: n -> count of edges => O(n)
// Space:  m - node length => O(m)
// var isBipartite = function(graph) {
  
//     // 0 -- unnset
//     // 1 -- set A
//     // 2 -- set B
//     const marks = new Array(graph.length).fill(0)
    
//     for (let i = 0; i < graph.length; i++) {
//       if (marks[i] === 0) {
//         // start a DFS from this node
//         marks[i] = 1
//         const stack = [i]
//         while (stack.length > 0) {
//           const top = stack.pop()
          
//           const nextMark = marks[top] === 1 ? 2 : 1
          
//           for (let nextNode of graph[top]) {
//             if (marks[nextNode] === 0) {
//               // not traversed yet
//               marks[nextNode] = nextMark
//               stack.push(nextNode)
//             } else if (marks[nextNode] !== nextMark) {
//               return false
//             }
//           }
//         }
//       }
//     }
  
//     return true
// };

// BFS still works
var isBipartite = function(graph) {
  
    // 0 -- unnset
    // 1 -- set A
    // 2 -- set B
    const marks = new Array(graph.length).fill(0)
    
    for (let i = 0; i < graph.length; i++) {
      if (marks[i] === 0) {
        // start a DFS from this node
        marks[i] = 1
        const queue = [i]
        while (queue.length > 0) {
          const head = queue.shift()
          
          const nextMark = marks[head] === 1 ? 2 : 1
          
          for (let nextNode of graph[head]) {
            if (marks[nextNode] === 0) {
              // not traversed yet
              marks[nextNode] = nextMark
              queue.push(nextNode)
            } else if (marks[nextNode] !== nextMark) {
              return false
            }
          }
        }
      }
    }
  
    return true
};
```
