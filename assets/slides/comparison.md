### Final Comparison

```sh
# plumbing
$ git hash-object -w test.txt
$ git update-index --add test.txt
$ git write-tree
$ echo "first commit" | git commit-tree 80865964295ae2f11d27383e5f9c0b58a8ef21da
$ git update-ref refs/heads/master 3a5a00a726b1710a9d50f8ad95aaa212c04739c0
$ git gc
$ git push origin master

# porcelain
$ git add test.txt
$ git commit -m "first commit"
$ git push origin master
```
