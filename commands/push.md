---
description: Git - pushing git branches to remote repository 
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git rebase:*)
---


# Commit - Git push rules
if not described in the global rules then follow the following rules  
for pushing code in vcs systems.

## Process:

### Branch naming strategy
All branches start with the JIRA ticket number and then a short  
description of the work that is being done.
For example: `JIRA-1234-fix-login-bug`

### Before pushing
- Before pushing all commits are squashed into one commit.

### Push to remote
Don't ask just push the commit to the remote repository:
```bash
git push origin <branch-name>
```

### After pushing: PR Templates
- PR templates are used to ensure that all PRs follow the same format.
- PR templates are always followed.
- Draft PR follow the PR templates from non draft PRs.
- If PR templates asked to fill in description then use the template below
```
### The problem:
Problem description here

### The solution:
Solution description here

### The reasoning behind the solution:
Reasoning behind the solution here
```
- Non Negotionable after pushing a new Draft PR is created following PR template guidelines mentioned above. Existing PRs are updated!


## Output

### Commit Created

**Commit Hash**: [hash]

**Commit Message**:
```
[full commit message]
```

**Files Committed**:
- [list of files with change stats]

**Summary**:
- X files changed
- Y insertions(+)
- Z deletions(-)

### PR Link
Report back the link of the PR created. 
If the PR is already created then report back the link of the existing PR.

## Notes
- If there are no changes to push, report this clearly
- If push fails, report the error
