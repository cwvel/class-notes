## Debugging
### Terminology
**Fault:** erroneous **location** in the code
$\Downarrow$ *program execution* 
**Error:** incorrect **state** during execution
$\Downarrow$ *error reaches system boundary*
**Failure:** observed incorrect **outside behavior** (e.g. crash, incorrect output displayed)
### Steps
#### 1. Reproduce the bug
- Recreate the problem environment
- Reproduce the problem history (steps to recreate the problem)
- Automated bug reproduction test
#### 2. Locate the faulty code
- Use logs, visual diagrams
- Get rid of code smells using refactoring before debugging
- Use assertions to prevent errors from propagating
#### 3. Determine the root cause
- Break points for debugging, observe program step by step
	- Conditional break points
#### 4. Implementing and verifying a fix
- Document bug fix and run your tests
- Keep all new tests for **regression testing**
	- ensures new updates haven't introduced bugs into existing functionality

## Advanced Git Techniques
### Detached `HEAD` state
- **Non-detached HEAD**: attached to branch; most git commands will move the branch and head
- **Detached HEAD**: pointing to (checked out) commit instead of branch, git commands will not move the branch
> *You are in 'detached HEAD' state. You can look around, make experimental changes and commit them, and you can discard any commits you make in this state without impacting any branches by switching back to a branch.*

### Relative commit addresses
- **Describe the parent/grandparent, etc. commit** without getting the commit ID from the log:
- `BRANCH~n` is the n-th commit before `BRANCH`

### `git cherry-pick`
- **Copy one particular commit from one branch to another** without bringing over the entire history
- `git cherry-pick β` calculates the difference (**patch**) for the commit $\beta$ and creates a new commit that applies that same patch to the current base
	- Can result in merge conflicts if patch not applied correctly

### `git stash & pop`
- Checkout a branch or commit while you have uncommitted changes (that you might want to commit either)
- `git stash` moves your changes to a separate stack and use `git stash pop` to bring them back
	- Every time `git stash` is called, Git adds the patches to the stack, and `git stash pop` removes them from the stack
- `git stash list` shows the entire stack
- `git stash apply <id>` applies a non-top stash patch

### `git blame`
- For a given line, identify **why it exists** and why it has been implemented the way it has, or **who has most recently changed this line**
- `git blame <filename>` tells you for each line
	- the **commit id** of the last commit that modified this line, the **author**, and **timestamp**
	- can be visualized by GitHub

### `git bisect`
- Out of hundreds of commit, find **which one introduced the bug**
- Suppose a past commit `c_good` passes the command `test` (e.g. `pytest`)
- Run: `git bisect start c_good && git bisect run test` *might be slightly different*
	- Git runs a binary search to find a past commit that broke the tests

### `git revert`
- To **undo** a commit in the history of your branch (like if it introduced a bug)
- `git revert B` calculates the patch for the commit `B` and create a new commit that applies the **inverse patch** to current base
	- Can result in merge conflicts if the inverse patch cannot be applied directly
	- **Non-destructive** (preserves history)

### `git rebase -i`: Interactive rebase
- Change your commit history to make it linear
	- `git rebase -i A` rewrites the commit history starting from commit A. If changes are made (e.g., commits should be dropped or added within a break) git creates new commits with the same patches
- Can be destructive - may lose your commits
	- Results in a **new commit history**
	- When working in teams, only use `git rebase -i` on commits that exist only on your local machine or on a feature branch that only you are working on

### `git rebase f`: Simple rebase
- Alternative to **merge**: merges a feature branch, but instead of a merge commit with two parents, you just "copy" the individual commits
- `git rebase f` combines the patches from all commits on the feature branch into one instead of creating a merge commit with two parents

![500](../../Pasted%20images/Pasted%20image%2020251124144125.png)


### `git merge --squash`: Squash merge
- Combines patches from all commits on the feature branch into one instead of creating a merge commit with two parents
- Keeps the history cleaner

### Git submodules
- Include **external libraries**/**shared modules** within your project while maintaining their history and keeping them separate from your main repository
- Clones another git repository inside of a specific directory (e.g. *dependencies*) in your repository
	- Holds a "pointer" to a commit of the cloned repository
- `git submodule add <repo-url> <path>`
	- Clones `<repo-url>` into `<path>` and starts tracking it as a submodule
- `git clone --recursive <repo-url>`
	- Clones `<repo-url>` and its submodules, checks out selected commit
- `git submodule update`
	- Reset submodule content to selected commit
- Committing content within the submodule
	1. Commit changes within the submodule folder and push
	2. Change directory to outside the submodule, commit the submodule and push
