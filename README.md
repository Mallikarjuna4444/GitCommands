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

### Git Cherry-pick

Git cherry-pick is a command used to apply a specific commit from one branch to another. It's particularly useful when you want to pick only certain commits instead of merging entire branches. Here’s how you typically use it:

1. **Find the commit hash**: Identify the commit you want to apply. You can find this using `git log` or by any other means to inspect your commit history.

2. **Switch to the target branch**: Make sure you are on the branch where you want to apply the commit. Use `git checkout <branch>` to switch branches if needed.

3. **Cherry-pick the commit**: Execute the command `git cherry-pick <commit-hash>`. Replace `<commit-hash>` with the actual hash of the commit you identified in step 1.

For example:
```
git cherry-pick abc12345
```

4. **Resolve conflicts (if any)**: If there are conflicts between the changes introduced by the cherry-picked commit and the current state of the branch, Git will pause and ask you to resolve them. You can use `git status` to see which files have conflicts, resolve them manually, add the resolved files (`git add <resolved-file>`), and then continue the cherry-pick with `git cherry-pick --continue`.

5. **Commit the cherry-pick**: Once conflicts are resolved (if any), Git will commit the changes with a default commit message or a message you can specify with the `-m` flag.

6. **Continue or abort**: If you encounter problems during cherry-pick, you can abort it with `git cherry-pick --abort`.

**Note**: 
- Cherry-picking copies the changes introduced by the specified commit to your current branch. It does not merge the entire branch.
- Avoid cherry-picking commits that have already been merged into your branch to prevent duplicate commits and confusion in your repository history.

This command is handy in scenarios where you want to selectively apply changes from one branch to another, such as backporting bug fixes or applying specific features developed in parallel branches.

### Git Rebase

Git rebase is a powerful command used to integrate changes from one branch into another by applying each commit from the current branch onto another branch. It essentially allows you to move or combine a sequence of commits to a new base commit, which is typically the head of another branch.

### Basic Usage of Git Rebase

1. **Switch to the target branch**: First, ensure you are on the branch where you want to apply the changes. For example, if you want to rebase `feature_branch` onto `main`, you would switch to `feature_branch`.

   ```bash
   git checkout feature_branch
   ```

2. **Start the rebase**: Initiate the rebase process by using `git rebase <base_branch>`. In this case, `<base_branch>` would be `main`.

   ```bash
   git rebase main
   ```

   Git will take each commit that is unique to the current branch (`feature_branch` in this case), save them to a temporary area, reset the current branch to the same commit as `<base_branch>`, and then sequentially apply each commit from the temporary area on top of the `<base_branch>`.

3. **Resolve conflicts (if any)**: If there are any conflicts between the changes made in your branch and the `<base_branch>`, Git will pause and ask you to resolve them. You can use `git status` to see which files have conflicts, resolve them manually, add the resolved files (`git add <resolved-file>`), and then continue the rebase with `git rebase --continue`.

4. **Complete the rebase**: Once all conflicts are resolved and all commits are applied, the rebase is complete. Git will automatically move your branch pointer (`feature_branch`) to the tip of `<base_branch>`.

5. **Push the rebased branch**: After successfully rebasing, you may need to force push (`git push --force`) the branch if you've rebased commits that have already been pushed to a remote repository.

### Advantages of Git Rebase

- **Linear History**: Rebasing can help maintain a cleaner and more linear project history compared to merging, as it applies commits one by one on top of another branch.
  
- **Easier to Understand History**: It can make it easier to understand the sequence of changes, especially in collaboration scenarios where multiple developers are working on the same repository.

- **Resolving Conflicts Early**: Rebasing forces you to resolve conflicts as each commit is applied, rather than all at once at the end of a merge.

### Considerations

- **Do Not Rebase Public Branches**: Avoid rebasing commits that have already been pushed to a remote repository and shared with others. This can lead to confusion and conflicts for other developers working on the same branch.

- **Use with Caution**: Rebase rewrites commit history, so use it with caution, especially in shared branches or repositories where others are collaborating.

Git rebase is particularly useful for maintaining a clean and linear history in your repository and integrating changes from one branch into another in a more controlled manner compared to traditional merging.

### Git Squah

Git squash is a technique used to combine multiple commits into a single commit. This is useful when you have a series of commits that logically belong together and you want to tidy up your commit history before merging or pushing changes. Squashing reduces the noise and makes the commit history more concise and easier to follow.

### How to Squash Commits

Here’s a step-by-step guide to squash commits using Git:

1. **Identify the commits to squash**: Determine which commits you want to squash together. You typically squash commits that are related and can be logically grouped into a single commit.

2. **Start an interactive rebase**: Use `git rebase -i HEAD~n`, where `n` is the number of commits you want to include in the interactive rebase. For example, if you want to squash the last 3 commits, you would use:

   ```bash
   git rebase -i HEAD~3
   ```

   This opens an interactive rebase window where you can specify actions for each commit.

3. **Specify squash for commits**: In the interactive rebase window that opens, you will see a list of commits with instructions. Change `pick` to `squash` (or just `s`) for all the commits except the first one. The first commit in the list will be preserved as is or can be marked as `pick`.

   For example:

   ```plaintext
   pick abc1234 First commit message
   squash def5678 Second commit message
   squash ghi91011 Third commit message
   ```

   This configuration tells Git to squash commits `def5678` and `ghi91011` into `abc1234`.

4. **Save and close the rebase file**: Save the changes and close the editor. Git will then combine the specified commits into one.

5. **Edit the commit message (if needed)**: Git will open another editor window where you can edit the combined commit message. This message can be a combination of the individual commit messages or a new message summarizing the changes.

6. **Finish the rebase**: Save and close the commit message editor. Git will complete the rebase process and apply the squashed commit with the new commit message.

7. **Push changes (if necessary)**: If you've already pushed the commits you've squashed, you may need to force push (`git push --force`) to update the remote branch with the squashed commit history. Be cautious with force pushing as it rewrites history and can cause issues for others collaborating on the same branch.

### Benefits of Squashing Commits

- **Cleaner History**: Squashing reduces the number of commits in the history, making it easier to understand and review the changes made over time.
  
- **Logical Grouping**: It allows you to group related changes into a single commit, maintaining a clear narrative of what was changed.

- **Preparation for Integration**: Squashing commits before merging into a main branch or pushing to a shared repository helps keep the repository's history clean and more manageable for other team members.

### Considerations

- **Use with Caution**: Squashing alters commit history, which can complicate collaboration if others have based work on the existing commits. Communicate with your team before squashing commits that have already been shared.

- **Preserve Meaningful History**: While squashing is beneficial for cleaning up minor commits, it's important to preserve meaningful commit history for major changes and features.

Squashing commits is a valuable technique in Git for maintaining a clean and structured commit history, especially when preparing changes for review, integration, or sharing with a team.




