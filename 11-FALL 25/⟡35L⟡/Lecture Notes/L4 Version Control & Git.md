# Git
![Pasted image 20251207182722](Pasted%20image%2020251207182722.png)

- `git config` = sets name, email, etc. at the beginning
- **Tree structures**
	- **Working tree**: current version of files (as in code editor)
	- **Local repo:** Complete history of all changes to the project
	- `git push` sends changes from local to remote repo
	- `git fetch` receives changes from remote to local (doesn't actually change files, must use `git merge`)
	- `git pull` = fetch and merge
	- `git reset --hard` = undo changes in working tree
- `git status` = describes branch, changes in staging area, other changes in working tree
- `git add <file1> ...` = adds changes in files to staging area
	- `git add -A` = adds all changes to staging area (even new files)
	- `git add .` = might not add deletions?
	- `git restore --staged` = take changes out of staging area without changing the working tree (undo of `git add`)
- `git commit`
	- `git commit -a` only commits tracked files (that have been committed before)
	- `git checkout <commit>` restores previous versions
- `.gitignore` must be committed first, specifies files to not track
- `origin` = remote repo
- `--amend` lets you edit a commit afterwards (author, which files, etc)

**Branches**
- A pointer to a commit
	- `HEAD` is the commit you are currently on
- `git branch new_branch` + `git checkout new_branch` to create and move to the new branch
- `git merge main` merges the commits from main into your current branch
- **Detached head** means it is pointing to a *commit* and not a *branch*
- **Merge conflicts**
	- `<<<<<<< HEAD` on your branch
	- `=======` separator
	- `>>>>>> branch_name` = the branch you had merge conflicts with
- **Add**
	- `-A` vs `-u` vs `.`

## Centralized vs. Distributed
![Pasted image 20251207182837](Pasted%20image%2020251207182837.png)
![Pasted image 20251207182856](Pasted%20image%2020251207182856.png)
