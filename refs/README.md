# Refs

Initialize the repository:

```console
$ git init

```

Create a tag:

```console
$ echo "tag" > file.txt && git add . && git commit -m "tag"
$ git tag v1.0
```

Create an annotated tag:

```console
$ echo "annotated-tag" > file.txt && git add . && git commit -m "annotated-tag"
$ git tag -a v2.0 -m "Tag v2.0"
```

Create branch:

```console
$ echo "branch" > file.txt && git add . && git commit -m "branch"
$ git branch branch
```

```console
$ find .git/refs -type f
.git/refs/heads/master
.git/refs/heads/branch
.git/refs/tags/v1.0
.git/refs/tags/v2.0
```

```console
$ git gc
```

```console
$ cat .git/packed-refs
# pack-refs with: peeled fully-peeled sorted
f2c6679f38b2bf8d5dc0f090a8a424d380b343fd refs/heads/branch
f2c6679f38b2bf8d5dc0f090a8a424d380b343fd refs/heads/master
c897fcef1ebd3179c4e166508166045e6d5bf4a0 refs/tags/v1.0
96fae537cfff7d797a21200dc1497e094d4fe0e9 refs/tags/v2.0
^e9ea1e0a0cd118317873f691a8cd015b9f78160d
```

![Git-Refs](git-refs.png)
