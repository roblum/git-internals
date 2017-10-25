### Create a Pack File
* `packfile` is a binary file containing loose objects.
* `git gc` - garbage collect. runs every push. this will combine all loose objects into one file and store deltas from one version to next. can reduce size.
* `verify-pack` can show what objects were packed in garbage collection.

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

@[1]
@[2]
@[3]
@[5-10]
