## Git Internals and Plumbing

---

### Plumbing vs Porcelain

| Plumbing | Porcelain |
|----------|-----------|
| Low level commands | User friendly |
| Chained together to form porcelain commands | Ex: `git add` |

---

## Create a Repository

```
> mkdir test-plumbing
> cd test-plumbing
> git init
```

---

### What is .git?

`.git` is a directory containing everything git stores and manipulates about the current repository. Cloning or backing up a repo can be done solely through .git.

```
> brew install tree
> tree .git
.git
├── HEAD
├── config
├── description
├── hooks
├── info
│   └── exclude
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags
```

---

### Important Internals
* `HEAD` is a file that points to the current checked out branch (also points to the last commit from that branch, see detached HEAD)
* `index` is a file that stores your staging information
* `objects` is a directory that stores all content from the repository
* `refs` is a directory storing pointers from any identifier (heads, tags, branches) to the latest commit hash.

---

### Creating a file

* `hash-object` stores the object with a header, and outputs a checksum hash (SHA-1).
* `cat-file` provides the content or type of an object. (-t type, -p contents, -s size)

```
> echo 'test content' > test.txt
> git hash-object -w test.txt
d670460b4b4aece5915caf5c68d12f560a9fe3e4

> git cat-file -p d670460b4b4aece5915caf5c68d12f560a9fe3e4
test content

// Verify hash is correct
> printf "blob 13\000test content\n" | openssl sha1
d670460b4b4aece5915caf5c68d12f560a9fe3e4
```

Raw content of object file (zlib compressed)
```
> cat .git/objects/d6/70460b4b4aece5915caf5c68d12f560a9fe3e4
xK??OR04f(I-.QH??+I?+?K?	%       
```

---

### Staging a file

```
> git update-index --add test.txt
> git ls-files --stage
100644 d670460b4b4aece5915caf5c68d12f560a9fe3e4 0	test.txt
```

---

### Commit the file

```
> git write-tree
80865964295ae2f11d27383e5f9c0b58a8ef21da
> git cat-file -p 80865964295ae2f11d27383e5f9c0b58a8ef21da

> echo "first commit" | git commit-tree 3a5a00a726b1710a9d50f8ad95aaa212c04739c0
> git cat-file -p 3a5a00a726b1710a9d50f8ad95aaa212c04739c0

> git status
```

---

### Attach the commit to a branch
`update-ref` updates a reference the passed object.

```
> git update-ref refs/heads/master <commit-SHA>
> cat .git/refs/heads/master
```

---

### Create a Pack File
`packfile` is a binary file containing loose objects.
`git gc` - garbage collect. runs every push. this will combine all loose objects into one file and store deltas from one version to next. can reduce size.
`verify-pack` can show what objects were packed in garbage collection.

```
> git count-objects -H
> git gc
> git count-objects -H
> git verify-pack -v .git/objects/pack/pack-d4eea996fc1b9bb9f8d26502e8203225497fb8bb.idx
3a5a00a726b1710a9d50f8ad95aaa212c04739c0 commit 173 120 12
d670460b4b4aece5915caf5c68d12f560a9fe3e4 blob   13 22 132
80865964295ae2f11d27383e5f9c0b58a8ef21da tree   36 47 154
non delta: 3 objects
.git/objects/pack/pack-d4eea996fc1b9bb9f8d26502e8203225497fb8bb.pack: ok
```
