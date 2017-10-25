### Creating a file

* `hash-object` stores the object with a header, and outputs a checksum hash (SHA-1).
* `cat-file` provides the content or type of an object. (-t type, -p contents, -s size)

```sh
$ echo 'test content' > test.txt
$ git hash-object -w test.txt
d670460b4b4aece5915caf5c68d12f560a9fe3e4

$ git cat-file -p d670460b4b4aece5915caf5c68d12f560a9fe3e4
test content

# Verify hash is correct
$ printf "blob 13\000test content\n" | openssl sha1
d670460b4b4aece5915caf5c68d12f560a9fe3e4

# Raw content of object file (zlib compressed)
$ cat .git/objects/d6/70460b4b4aece5915caf5c68d12f560a9fe3e4
xK??OR04f(I-.QH??+I?+?K?	%
```

@[1]
@[2-3]
@[5-6]
@[8-14]
