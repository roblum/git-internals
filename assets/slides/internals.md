### Important Internals
* `HEAD` is a file that points to the current checked out branch (also points to the last commit from that branch or [detached head](https://git-scm.com/docs/git-checkout#_detached_head)).
* `index` is a file that stores your staging information.
* `objects` is a directory that stores all content from the repository.
* `refs` is a directory storing pointers from any identifier (heads, tags, branches) to the latest commit hash.
