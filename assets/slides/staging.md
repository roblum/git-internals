### Adding files to Staging
`update-index` adds the file contents from the working tree to the index file.

```sh
$ git update-index --add test.txt
$ git ls-files --stage
100644 d670460b4b4aece5915caf5c68d12f560a9fe3e4 0	test.txt
```

@[1]
@[2-3]
