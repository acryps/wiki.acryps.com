# Git Commits
Git messages should always be prefixed with `Add`, `Fix` or `Merge` - except for the `Initial commit`.

A commit message can exceed the recommended message length limit.

A git message should not state the obvious, like `Add index.html`. We know that `index.html` was added, it is already in the change index. It should describe what or why it happened - `Add home page`. 

- `Fix typo` should only be used when actually fixing a typo
- `.` is never valid.
- `Fix some issues` is never valid
- `Fix bug` neither.

Use english messages, even in localized source code.

## Background for the prefixes
We used to use `add` and `fix`. In the source code of git, `Merge` is capitalized when automatically generating the merge commit (`fmt_merge_msg_title` in `fmt-merge-msg.c`). Thus we updated the prefixes to be capitalized.