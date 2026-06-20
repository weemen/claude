---
description: Create git commit with conventional message format
argument-hint: [file1] [file2] ... (optional - commits all changes if not specified)
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git rebase:*)
---


# Commit - Git commit rules 
if not described in the global rules then follow the following rules  
for commiting code in vcs systems.

## Process:
### Files to Commit

Files specified: $ARGUMENTS

(If no files specified, will commit all changes)

### Branch naming strategy
All branches start with the JIRA ticket number and then a short  
description of the work that is being done.
For example: `JIRA-1234-fix-login-bug`

### Before committing
Before commiting validate that:
- the code is working
- the code is tested
- the code is documented
- the code is formatted
- the code is linted

### Review Current State

Check git status:
!`git status`

Review changes to commit:
!`git diff HEAD`

If staging specific files, review their changes:
!`git diff HEAD -- $ARGUMENTS`

### Stage Files

If specific files provided:
```bash
git add $ARGUMENTS
```

If no files specified (commit all changes):
```bash
git add .
```

### Commit messages
Commit messages start with the JIRA ticket number and then a one line 
sentence of the work that is being done.
After the one line follows three dashes and a description header with a longer description of the work.
Follow the example below: 
```
JIRA-1234 fixed logic to login via SSO:
---
Description:
- added logic to login via SSO
- refactored login logic to make it more readable
```

## Output

### Push to remote
Push the commit to the remote repository:
```bash
git push origin <branch-name>
```

### PR Templates
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
- Upon PR creation all commits are squashed into one commit unless there is already a PR open.
- When squashing commits, the smashed commit message should follow the commit message guidelines.

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

## Notes

- If there are no changes to commit, report this clearly
- If commit fails (e.g., pre-commit hooks), report the error
- Follow the project's commit message conventions
- Include co-author if appropriate:
  ```
  Co-authored-by: Claude <noreply@anthropic.com>
  ```