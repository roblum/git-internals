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