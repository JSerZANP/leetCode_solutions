Me explaining this on youtube: https://youtu.be/nAVs5jAhWlU

```js
/**
 * @param {string[][]} accounts
 * @return {string[][]}
 */
var accountsMerge = function(accounts) {
    //  list 1 => user 1   email1 email2
    //  list 2 => user 2   email3 email4
    //  list 3 => user 3   email3 email4
    // ...
    // for each list, check if email is used or not, if so, merge the user
     // User < name, emails>
    // Map<email, user>
    // Set<User>, to merge, update the emails of user, update Map<email, user>
    
    const users = new Set()
    // for User, ['name', Set<email:string>]
    const emailUserMap = new Map()
    
    const merge = (userFrom, userTo) => {
      if (userFrom === userTo) return
      users.delete(userFrom)
      
      // update all the email , link to userTo
      // add email to userTo
      
      for (let email of userFrom[1]) {
        emailUserMap.set(email, userTo)
        userTo[1].add(email)
      }
    }
    
    for (let account of accounts) {
      const [name, ...emails] = account
      const user = [name, new Set()]
      users.add(user)
      for (let email of emails) {
        if (emailUserMap.has(email)) {
          merge(emailUserMap.get(email), user)
        } else {
          emailUserMap.set(email, user)
          user[1].add(email)
        }
      }
    }
    
    const result = []
    
    for (let user of users) {
      const list = [...user[1]].sort()
      list.unshift(user[0])
      result.push(list)
    }
    
    return result
};
```
