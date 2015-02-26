# Git Hooks
A collection of git hooks.
- [Overview](#overview)
- [Activation](#activation)
- [Hooks](#hooks)
    - [post-checkout](#post-checkout)

<a name="overview" id="overview"></a>
## Overview
[Git hooks](http://git-scm.com/docs/githooks) are commands that 'hook' into git and run automatically when a specific git command is issued. These are some hooks that I like to use.
- [post-checkout](#post-checkout): This hook is invoked when a `git checkout` (or `git clone`) is run, after having updated the worktree

<a name="activation" id="activation"></a>
## Activation
To activate these git-hooks, copy them into:
<br>
`<YOUR_CHECKOUT_DIRECTORY>/.git/hooks`

Be sure to enable the correct permissions (they must be executable)
<br>
`chmod 755 <hook file>`

<a name="hooks" id="hooks"></a>
## Hooks
This a list of hooks that have been modified and what they do when activated.

<a name="post-checkout" id="post-checkout"></a>
#### post-checkout
After a `git checkout` (or a `git clone`), this will delete all the `.pyc` and `.pyo` files found, starting from the repository root.
```
#!/bin/sh
#
# This hook is invoked when a 'git checkout' (or 'git clone') is run, after having updated the worktree
# Start from the repository root and do the following:
# delete all .pyc and .pyo files

cd ./$(git rev-parse --show-cdup)

# Delete .pyc and .pyo files
find . -name "*.pyc" -delete
find . -name "*.pyo" -delete
# Delete all empty directories
# find . -type d -empty -delete
```
