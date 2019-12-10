# Git Submodule

Is it possible to add a submodule to a Git repository by hand? That is, just by
editing files in a text editor, not touching the Git CLI at all?

[I don't think so](https://stackoverflow.com/a/59273805/2715716):

When a submodule is added, Git creates `.submodules` file and for a submodule
named `git-submodule`, it will contain something like this:

```
[submodule "git-submodule"]
	path = git-submodule
	url = https://github.com/TomasHubelbauer/git-submodule
```

The same is added to `.git/config` after the existing content of that file.

A directory for the submodule named after the submodule is created in
`.git/modules`. This folder is nearly identical to the the `.git` directory of
the actual submodule repository, but it doesn't contain the actual `objects`
(instead the submodule data is checked out to its directory and its metadata
are here).

This means that theoretically, you might be able to add a submodule by hand
without using `git submodule add`, but you would have to recreate all these
config files.

But one can still imagine cloning the submodule repository to a separate
directory and copying its `.git` over to this one. That _might_ work.

However, adding a submodule also changes the index, `.git/index`, so you would
have to manually update this hash as well, and at this point, you're reimplementing
Git, but manually.

As a result, I don't believe it is anywhere near practical to add a Git submodule
by hand.
