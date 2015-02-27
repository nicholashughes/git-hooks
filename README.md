# Git Hooks
A collection of git hooks.
- [Overview](#overview)
- [Activation](#activation)
- [Hooks](#hooks)
    - [prepare-commit-msg](#prepare-commit-msg)
    - [post-checkout](#post-checkout)

<a name="overview" id="overview"></a>
## Overview
[Git hooks](http://git-scm.com/docs/githooks) are commands that 'hook' into git and run automatically when a specific git command is issued. These are some hooks that I like to use.
- [prepare-commit-msg](#prepare-commit-msg): This hook is invoked by `git commit` right after preparing the default log message, and before the editor is started
- [post-checkout](#post-checkout): This hook is invoked when a `git checkout` (or `git clone`) is run, after having updated the worktree

<a name="activation" id="activation"></a>
## Activation
To activate these git-hooks, copy them into:
<br>
`<YOUR_LOCAL_PROJECT_DIRECTORY>/.git/hooks`

Be sure to enable the correct permissions (they must be executable)
<br>
`chmod 755 <hook file>`

<a name="hooks" id="hooks"></a>
## Hooks
This a list of hooks that have been modified and what they do when activated.

<a name="prepare-commit-msg" id="prepare-commit-msg"></a>
#### prepare-commit-msg
This hook will prepend the branch name and branch description to every commit message. For example:
<br>
`[Branch Name] <Commit message entered in the editor>`

```
#!/bin/bash

# This way you can customize which branches should be skipped when
# prepending commit message.
if [ -z "$BRANCHES_TO_SKIP" ]; then
  #BRANCHES_TO_SKIP=(master develop test)
  BRANCHES_TO_SKIP=()
fi

BRANCH_NAME=$(git symbolic-ref --short HEAD)
BRANCH_NAME="${BRANCH_NAME##*/}"

BRANCH_EXCLUDED=$(printf "%s\n" "${BRANCHES_TO_SKIP[@]}" | grep -c "^$BRANCH_NAME$")
BRANCH_IN_COMMIT=$(grep -c "\[$BRANCH_NAME\]" $1)

if [ -n "$BRANCH_NAME" ] && ! [[ $BRANCH_EXCLUDED -eq 1 ]] && ! [[ $BRANCH_IN_COMMIT -ge 1 ]]; then
  sed -i.bak -e "1s/^/[$BRANCH_NAME] /" $1
fi
```
Note: This code came from this [gist](https://gist.github.com/bartoszmajsak/1396344)

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
