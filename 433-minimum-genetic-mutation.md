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
