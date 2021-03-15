Here is my video of explaining this: https://youtu.be/M4rMLK3Kn3w

```js
const numberToWords = (num) => {
  if (num === 0) return 'Zero'
  
  const numStr = num.toString()
  
  const result = []
  
  const words = {
    single: ['', 'One', 'Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine'],
    special: ['Ten', 'Eleven', 'Twelve', 'Thirteen', 'Fourteen', 'Fifteen', 'Sixteen', 'Seventeen', 'Eighteen', 'Nineteen'],
    double: ['', '', 'Twenty', 'Thirty', 'Forty', 'Fifty', 'Sixty', 'Seventy', 'Eighty', 'Ninety']
  }
  
  const bases = ['Billion','Million', 'Thousand', '']
  
  // cache the words in segments of 3
  const buffer = []
  
  const flush = () => {
    const base = bases.pop()
    
    if (buffer.length === 0) return
    
    
    if (base) {
      result.push(base)
    }
    result.push(...buffer)
    buffer.length = 0
  }
  
  for (let i = numStr.length - 1; i > -1; i--) {
    const mod = (numStr.length - 1 - i) % 3
    const char = numStr[i]
    switch (mod) {
      case 0:
        // if not the start, then need to flush the buffer
        // 1234 => 4,3,2, 1
        if (i !== numStr.length - 1) {
          flush()
        }
        
        // handle the first digit
        // 0, 1, 2 ... 9
        // special case if next one is '1`
        if (numStr[i - 1] === '1') {
          buffer.push(words.special[char])
          i -= 1
        } else {
          if (char !== '0') {
            buffer.push(words.single[char])
          }
        }
        break
      case 1:
        // for 20, 34, 99, 00(skip)
        if (char === '0') continue
        
        buffer.push(words.double[char])
        
        break
      case 2:
        if (char === '0') continue
        
        buffer.push('Hundred')
        buffer.push(words.single[char])
        break
    }
  }
  
  flush()
  
  return result.reverse().join(' ')
  
}
```
