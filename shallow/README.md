## DEV-DOC .git/shallow

### Shallow clone

Cloning a repositry means that you get every revision of every file ever committed.
On a large repository with a long history this can be a lot.

You can restrict the clone to a depth, which means that you truncate the history to
the specified number of commits.

```
git clone --depth 5 https://github.com/isomorphic-git/isomorphic-git'

git clone [remote-url] --branch [name] --single-branch [folder]
```

or with isomorphic-git:

```
await git.clone({
  fs,
  http,
  dir: '/tutorial',
  url: 'https://github.com/isomorphic-git/isomorphic-git',
  depth: 5
})
```

You can also restrict the clone to a certain branch:

```
git clone https://github.com/isomorphic-git/isomorphic-git' --branch main --single-branch
```

or with isomorphic-git:

```
await git.clone({
  fs,
  http,
  dir: '/tutorial',
  url: 'https://github.com/isomorphic-git/isomorphic-git',
  singleBranch: true,
  ref: 'main'
})
```

You can combine the depth and the branch restrictions.

### Shallow commits

In your shallow repository you get commits which have parents in the origin but repo
but not in the clone. So you cannot simply follow parent commit.

To solve this problem the `.git/shallow` file exist. It contains a list of commit hashes.

A commit, which has a parent commit which is contained in the `.git/shallow` file, should be
interpreted as a root commit, which has no parent.

![Shallow](shallow.png)
