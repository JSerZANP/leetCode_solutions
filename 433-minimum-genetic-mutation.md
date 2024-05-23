```js
/**
 * @param {string} startGene
 * @param {string} endGene
 * @param {string[]} bank
 * @return {number}
 */
class Node {
  mutations = new Set();
  constructor(gene) {
    this.gene = gene;
  }
}
var minMutation = function (startGene, endGene, bank) {
  // construct a graph
  const geneMap = new Map();

  function getOrCreateNode(gene) {
    if (geneMap.has(gene)) {
      return geneMap.get(gene);
    }
    const node = new Node(gene);
    geneMap.set(gene, node);
    return node;
  }

  const genes = [startGene, ...bank];
  for (let i = 0; i < genes.length - 1; i++) {
    for (let j = i + 1; j < genes.length; j++) {
      if (isMutation(genes[i], genes[j])) {
        const nodeI = getOrCreateNode(genes[i]);
        const nodeJ = getOrCreateNode(genes[j]);
        nodeI.mutations.add(nodeJ);
        nodeJ.mutations.add(nodeI);
      }
    }
  }

  const visited = new Set();
  const queue = [getOrCreateNode(startGene)];
  let mutationCount = 0;

  while (queue.length > 0) {
    let length = queue.length;
    while (length > 0) {
      const head = queue.shift();
      if (head.gene === endGene) {
        return mutationCount;
      }

      visited.add(head);
      for (const node of head.mutations) {
        if (!visited.has(node)) {
          queue.push(node);
        }
      }

      length -= 1;
    }
    mutationCount += 1;
  }

  return -1;
};

function isMutation(a, b) {
  if (a === b) return false;
  let diffCount = 0;
  for (let i = 0; i < a.length; i++) {
    if (a[i] !== b[i]) {
      diffCount += 1;
    }
    if (diffCount > 1) {
      return false;
    }
  }
  return true;
}
```

Another try in 2024

```js
/**
 * @param {string} startGene
 * @param {string} endGene
 * @param {string[]} bank
 * @return {number}
 */
var minMutation = function (startGene, endGene, bank) {
  // one mutation => count the indices where digits are different
  // shortest -> BFS

  // undirectional GRAPH
  // edge => only one mutation
  // we'll calculate the edges for startGene | bank

  // Map<string, Set<string>>
  const graph = new Map();

  const createEdge = (from, to) => {
    if (!graph.has(from)) {
      graph.set(from, new Set());
    }
    graph.get(from).add(to);
    if (!graph.has(to)) {
      graph.set(to, new Set());
    }
    graph.get(to).add(from);
  };

  for (let i = 0; i < bank.length - 1; i++) {
    for (let j = i + 1; j < bank.length; j++) {
      if (isMutation(bank[i], bank[j])) {
        createEdge(bank[i], bank[j]);
      }
    }
  }

  if (!graph.has(startGene)) {
    for (let i = 0; i < bank.length; i++) {
      if (bank[i] === startGene) {
        return -1;
      }

      if (isMutation(bank[i], startGene)) {
        createEdge(bank[i], startGene);
      }
    }
  }

  const queue = [startGene];
  const visited = new Set();
  let steps = 0;

  while (queue.length > 0) {
    let count = queue.length;
    while (count > 0) {
      const head = queue.shift();
      if (head === endGene) {
        return steps;
      }

      if (!visited.has(head)) {
        visited.add(head);
        const nodes = graph.get(head);
        if (nodes != null) {
          nodes.forEach((gene) => {
            queue.push(gene);
          });
        }
      }

      count -= 1;
    }
    steps += 1;
  }

  return -1;
};

function isMutation(from, to) {
  let differences = 0;
  for (let i = 0; i < from.length; i++) {
    if (from[i] !== to[i]) {
      differences += 1;
    }
    if (differences > 1) {
      return false;
    }
  }
  return true;
}
```
