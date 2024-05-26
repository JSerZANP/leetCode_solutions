```js
/**
 * @param {number} n
 * @param {number[][]} edges
 * @param {number[]} succProb
 * @param {number} start_node
 * @param {number} end_node
 * @return {number}
 */
var maxProbability = function (n, edges, succProb, start_node, end_node) {
  // suppose there is this best path from star to end
  // then for each node on the path, the path is the best path

  // so and edge [from, to] could actually help update the best path to [start, to]
  // but [start, from] must be the best as well

  // for the graph
  // we get the first layer of nodes, A, B, C
  // we can update the best path to each of them

  // now for A, it might connect to some other nodes, then we update them
  // or it connects to B, C, we update them them as well
  // for B, we do the same, but if we update A again, we need to repeat the process

  // but we need to avoid circles
  // is it enough we just track a visited set?
  // when it is in the set, it means we've already found the best path to it
  // if we update an existing node in the visited, we remove it from the visited and step on it again
  // so it will only actually affects the new best routes.

  const graph = new Map();
  for (let i = 0; i < edges.length; i++) {
    const [from, to] = edges[i];
    if (!graph.has(from)) {
      graph.set(from, new Set());
    }
    if (!graph.has(to)) {
      graph.set(to, new Set());
    }
    graph.get(from).add([to, succProb[i]]);
    graph.get(to).add([from, succProb[i]]);
  }

  const probs = new Map();
  probs.set(start_node, 1);

  const visited = new Set();

  const queue = [start_node];
  while (queue.length > 0) {
    const from = queue.shift();
    if (graph.has(from) && !visited.has(from)) {
      graph.get(from).forEach(([to, prob]) => {
        // if already visited, need to check if we need to go deeper
        const currProb = probs.get(from) * prob;
        const prevProb = probs.get(to) ?? 0;
        if (currProb > prevProb) {
          probs.set(to, currProb);
          queue.push(to);
          visited.delete(to);
        }
      });
    }
    visited.add(from);
  }

  return probs.get(end_node) ?? 0;
};
```
