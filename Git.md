## Repository
```bash
git init                # Initialize a new Git Repo
git clone <repo-url>    # Clone a Repo from URL
```
## Basics
```bash
git status              # Show Changes Status
git add <file>          # Add Changes to Staging
git commit -m "Message" # Commit changes with a message
git log                 # View Commit History
```
## Branching
```bash
git branch                     # List branches
git branch <branch-name>       # Create a new branch
git checkout <branch-name>     # Switch to a branch
git merge <branch-name>        # Merge changes from a branch
git branch -d <branch-name>    # Delete a branch
```
## Remote Repositories
```bash
git remote                     # List remotes
git remote add <name> <url>    # Add a remote
git push <remote> <branch>     # Push changes to a remote
```
## Undoing Changes
```bash
git pull                       # Fetch and merge changes
git reset --hard HEAD          # Discard changes without merging
git revert <commit-hash>       # Revert changes in a commit
```
