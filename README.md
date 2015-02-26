# Git Hooks
A collection of git hooks.
- [Overview](#overview)
- [Activation](#activation)
- [Hooks](#hooks)

<a name="overview" id="overview"></a>
## Overview
[Git hooks](http://git-scm.com/docs/githooks) are commands that 'hook' into git and run automatically when a specific git command is issued. These are some hooks that I like to use.

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
