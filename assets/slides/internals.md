### Important Internals
* `HEAD` is a file that points to the current checked out branch (also points to the last commit from that branch, see detached HEAD)
* `index` is a file that stores your staging information
* `objects` is a directory that stores all content from the repository
* `refs` is a directory storing pointers from any identifier (heads, tags, branches) to the latest commit hash.
