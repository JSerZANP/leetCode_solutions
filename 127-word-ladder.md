And here a video explaining this: https://youtu.be/pmImer7O3pM

```js
/**
 * @param {string} beginWord
 * @param {string} endWord
 * @param {string[]} wordList
 * @return {number}
 */

// n word, k letters
// Time: O(n^2)
// space: O(n^2)
var ladderLength = function(beginWord, endWord, wordList) {
    
    // 1. pre proces the wordList create a graph
    
    // O(k)
    const isTransformable = (word1, word2) => {
        // count the different letters
        let isDifferenceFound = false
        for (let i = 0; i < word1.length; i++) {
            if (word1[i] !== word2[i]) {
                if (isDifferenceFound) {
                    return false
                }
                isDifferenceFound  = true
            }
        }
        
        return true
    }
    
    // Map<string, Set<string>>
    // O(n^2) space
    const transformable = new Map()
    
    let isEndWordFound = wordList[wordList.length - 1] === endWord
    
    // O(n^2) time
    for (let i = 0; i < wordList.length - 1; i++) {
        if (wordList[i] === endWord) isEndWordFound = true
        for (let j = i + 1; j < wordList.length; j++) {
            if (isTransformable(wordList[i], wordList[j])) {
                if (transformable.has(wordList[i])) {
                    transformable.get(wordList[i]).add(wordList[j])
                } else {
                    transformable.set(wordList[i], new Set([wordList[j]]))
                }
                
                if (transformable.has(wordList[j])) {
                    transformable.get(wordList[j]).add(wordList[i])
                } else {
                    transformable.set(wordList[j], new Set([wordList[i]]))
                }
            }
        }
    }
    

    // a) return immediately if endWord is not in the list
    if (!isEndWordFound) return 0
    // 2. BFS it backwords, check the path length for all the words from endEowrd
    
    // Map<word, steps>
    // O(n) space
    const stepsMap = new Map()
    
    // O(n) space
    const queue = [endWord]
    let steps = 1
    
    // O(n^2) time
    while (queue.length  > 0) {
        queue.push(null)
        let head
        while (head = queue.shift()) {
            stepsMap.set(head, steps)
            
            const nextWords = transformable.get(head)
            
            if (nextWords) {
                for (let next of nextWords) {
                    if (!stepsMap.has(next)) {
                        queue.push(next)
                        stepsMap.set(next, 0)
                    }
                }
            }
        }
        
        steps += 1
    }
    
    
    // 3. match beginWord against all
    let result = Infinity
    for (let [word, steps] of stepsMap) {
        if (isTransformable(word, beginWord)) {
            result  = Math.min(result, steps + 1)
        }
    }
    
    return result === Infinity ? 0 : result
};
    
    
    
    
    
    
    
    
    
    
```
