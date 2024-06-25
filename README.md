### Git Commands

--

### Getting & Creating Projects

| Command | Description |
| ------- | ----------- |
| `git init` | Initialize a local Git repository |
| `git clone ssh://git@github.com/[username]/[repository-name].git` | Create a local copy of a remote repository |

### Basic Snapshotting

| Command | Description |
| ------- | ----------- |
| `git status` | Check status |
| `git add [file-name.txt]` | Add a file to the staging area |
| `git add -A` | Add all new and changed files to the staging area |
| `git commit -m "[commit message]"` | Commit changes |
| `git rm -r [file-name.txt]` | Remove a file (or folder) |

### Branching & Merging

| Command | Description |
| ------- | ----------- |
| `git branch` | List branches (the asterisk denotes the current branch) |
| `git branch -a` | List all branches (local and remote) |
| `git branch [branch name]` | Create a new branch |
| `git branch -d [branch name]` | Delete a branch |
| `git push origin --delete [branch name]` | Delete a remote branch |
| `git checkout -b [branch name]` | Create a new branch and switch to it |
| `git checkout -b [branch name] origin/[branch name]` | Clone a remote branch and switch to it |
| `git branch -m [old branch name] [new branch name]` | Rename a local branch |
| `git checkout [branch name]` | Switch to a branch |
| `git checkout -` | Switch to the branch last checked out |
| `git checkout -- [file-name.txt]` | Discard changes to a file |
| `git merge [branch name]` | Merge a branch into the active branch |
| `git merge [source branch] [target branch]` | Merge a branch into a target branch |
| `git stash` | Stash changes in a dirty working directory |
| `git stash clear` | Remove all stashed entries |

### Sharing & Updating Projects

| Command | Description |
| ------- | ----------- |
| `git push origin [branch name]` | Push a branch to your remote repository |
| `git push -u origin [branch name]` | Push changes to remote repository (and remember the branch) |
| `git push` | Push changes to remote repository (remembered branch) |
| `git push origin --delete [branch name]` | Delete a remote branch |
| `git pull` | Update local repository to the newest commit |
| `git pull origin [branch name]` | Pull changes from remote repository |
| `git remote add origin ssh://git@github.com/[username]/[repository-name].git` | Add a remote repository |
| `git remote set-url origin ssh://git@github.com/[username]/[repository-name].git` | Set a repository's origin branch to SSH |

### Inspection & Comparison

| Command | Description |
| ------- | ----------- |
| `git log` | View changes |
| `git log --summary` | View changes (detailed) |
| `git log --oneline` | View changes (briefly) |
| `git diff [source branch] [target branch]` | Preview changes before merging |

### Git Cheat Sheet

https://www.geeksforgeeks.org/git-cheat-sheet/

### Git Cheery-pick

Git cherry-pick is a command used to apply a specific commit from one branch to another. It's particularly useful when you want to pick only certain commits instead of merging entire branches. Here’s how you typically use it:

1. **Find the commit hash**: Identify the commit you want to apply. You can find this using `git log` or by any other means to inspect your commit history.

2. **Switch to the target branch**: Make sure you are on the branch where you want to apply the commit. Use `git checkout <branch>` to switch branches if needed.

3. **Cherry-pick the commit**: Execute the command `git cherry-pick <commit-hash>`. Replace `<commit-hash>` with the actual hash of the commit you identified in step 1.

For example:
```bash
git cherry-pick abc12345
```

4. **Resolve conflicts (if any)**: If there are conflicts between the changes introduced by the cherry-picked commit and the current state of the branch, Git will pause and ask you to resolve them. You can use `git status` to see which files have conflicts, resolve them manually, add the resolved files (`git add <resolved-file>`), and then continue the cherry-pick with `git cherry-pick --continue`.

5. **Commit the cherry-pick**: Once conflicts are resolved (if any), Git will commit the changes with a default commit message or a message you can specify with the `-m` flag.

6. **Continue or abort**: If you encounter problems during cherry-pick, you can abort it with `git cherry-pick --abort`.

**Note**: 
- Cherry-picking copies the changes introduced by the specified commit to your current branch. It does not merge the entire branch.
- Avoid cherry-picking commits that have already been merged into your branch to prevent duplicate commits and confusion in your repository history.

This command is handy in scenarios where you want to selectively apply changes from one branch to another, such as backporting bug fixes or applying specific features developed in parallel branches.




