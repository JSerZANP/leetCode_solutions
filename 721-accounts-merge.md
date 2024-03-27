## 1. Keep merging the account by emails

Me explaining this on youtube: https://youtu.be/nAVs5jAhWlU

```js
/**
 * @param {string[][]} accounts
 * @return {string[][]}
 */
var accountsMerge = function (accounts) {
  //  list 1 => user 1   email1 email2
  //  list 2 => user 2   email3 email4
  //  list 3 => user 3   email3 email4
  // ...
  // for each list, check if email is used or not, if so, merge the user
  // User < name, emails>
  // Map<email, user>
  // Set<User>, to merge, update the emails of user, update Map<email, user>

  const users = new Set();
  // for User, ['name', Set<email:string>]
  const emailUserMap = new Map();

  const merge = (userFrom, userTo) => {
    if (userFrom === userTo) return;
    users.delete(userFrom);

    // update all the email , link to userTo
    // add email to userTo

    for (let email of userFrom[1]) {
      emailUserMap.set(email, userTo);
      userTo[1].add(email);
    }
  };

  for (let account of accounts) {
    const [name, ...emails] = account;
    const user = [name, new Set()];
    users.add(user);
    for (let email of emails) {
      if (emailUserMap.has(email)) {
        merge(emailUserMap.get(email), user);
      } else {
        emailUserMap.set(email, user);
        user[1].add(email);
      }
    }
  }

  const result = [];

  for (let user of users) {
    const list = [...user[1]].sort();
    list.unshift(user[0]);
    result.push(list);
  }

  return result;
};
```

## 2. Graph Traversal

Think of the Account and Email as types of node, they form a Graph.
Each time we start from one Account and find all the connected account by dfs.

```js
/**
 * @param {string[][]} accounts
 * @return {string[][]}
 */

class NodeAccount {
  emails = new Set();
  constructor(name) {
    this.name = name;
  }
}

class NodeEmail {
  accounts = new Set();
  constructor(email) {
    this.email = email;
  }
}

var accountsMerge = function (accounts) {
  // suppose we have two kinds of node
  // 1. account
  // 2. email

  // then we form a graph where edges are between account and email
  // we need map account node to canonical account.

  // for each account we traverse all the connected nodes
  // each round we are able to get one canonical account.

  // in the end we'll get the all the canonical account after dedup
  const emailNodes = new Map();
  const accountNodes = new Set();
  const canonicals = new Set();

  function getEmailNode(email) {
    if (emailNodes.has(email)) {
      return emailNodes.get(email);
    }
    const node = new NodeEmail(email);
    emailNodes.set(email, node);
    return node;
  }

  function createAccountNode(name) {
    const accountNode = new NodeAccount(name);
    accountNodes.add(accountNode);
    return accountNode;
  }

  function createCanonicalAccountNode(name) {
    const accountNode = new NodeAccount(name);
    canonicals.add(accountNode);
    return accountNode;
  }

  for (const [name, ...emails] of accounts) {
    const accountNode = createAccountNode(name);
    for (const email of emails) {
      const emailNode = getEmailNode(email);
      emailNode.accounts.add(accountNode);
      accountNode.emails.add(email);
    }
  }

  function walk(node, canonical) {
    // processed
    if (node.canonical) {
      if (node.canonical !== canonical) {
        throw new Error("node.canonical should be same as current arge");
      }
      return;
    }
    node.canonical = canonical;
    if (node instanceof NodeAccount) {
      // merge the account into canonical
      const emails = node.emails;
      for (const email of emails) {
        canonical.emails.add(email);
        walk(getEmailNode(email), canonical);
      }
    } else {
      for (const accountNode of node.accounts) {
        walk(accountNode, canonical);
      }
    }
  }

  for (const accountNode of accountNodes) {
    if (accountNode.canonical == null) {
      const canonical = createCanonicalAccountNode(accountNode.name);
      walk(accountNode, canonical);
    }
  }

  const result = [];
  for (const accountNode of canonicals) {
    const emails = [...accountNode.emails];
    emails.sort((a, b) => {
      if (a === b) throw new Error("should be no duplicate in email list");
      if (a < b) return -1;
      return 1;
    });
    result.push([accountNode.name, ...emails]);
  }

  return result;
};
```
