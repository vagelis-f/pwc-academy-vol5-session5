# Git Workshop

## 1. What is Git?

Git is a version control system that tracks changes to your code over time. It allows you to:
- Save different versions of your project
- Collaborate with other developers
- Revert to previous versions if needed
- Work on different features simultaneously

## 2. Git vs GitHub
| Feature               | Git                                        | GitHub                                          |
|-----------------------|---------------------------------------------|--------------------------------------------------|
| What it is            | A tool installed on your computer           | A online  platform for hosting Git repositories  |
| Primary purpose       | Track and manage changes in code            | Store, share, and collaborate on Git repos       |
| Requires internet?    | ❌ No                                       | ✔️ Yes                                           |
| Works without Git?    | —                                           | ❌ No (GitHub depends on Git)                    |
| Works without GitHub? | ✔️ Yes                                      | —                                                |


## 3. Start working on a New Git Repository
A repository is the project’s storage space.
It contains:
- Project files
- All previous versions of those files (history)
- Branches, tags, and other Git metadata

Repos can be:
- **Local** - stored on your computer
- **Remote** - stored on an online platform like GitHub

### Option 1: Initialize a new git repository
Start a Git project on your local machine from scratch.

```bash
git init                     # Initialize a new Git repository locally
git remote add origin <url>  # Link the local repo to a remote repository
```

### Option 2:  Clone an existing repository
Download a copy of a remote repository to your local machine.

```bash
git clone <url>
```

### Option 3: Fork an existing repository
A fork is your own copy of someone else’s repository. Use it when:
- You don’t have write access
- You want a safe place to experiment without affecting the original project

**How to a Fork the Repository:**
1. Go to the original repository in Github
2. Click the "Fork" Button
3. Choose a repository name & description
4. Uncheck "Copy the main branch only" option
4. Click on "Create Fork"
5. Clone Your Fork Locally:  `git clone <fork-url>`

Today's repo is: 
https://github.com/stellavl/pwc-academy-vol5-session5

## 4. Work locally
### 4.1 Check Status & History
```bash
git status                 # See which files have changed
git log                    # View commit history
```

### 4.2 Stage Changes
```bash
git add <file>             # Stage specific file
git add .                  # Stage all changes
```

### 4.3 Commit Changes
```bash
git commit -m "message"    # Save changes with a description
```

#### Commit Message Best Practices
- Use present tense: "Add feature" instead of "Added feature"
- Be specific about what changed: "Fix login button alignment" not "Fix bug"
- Keep it short but clear

Example: `git commit -m "Add user authentication to login page"`

### 4.4 Undo Changes & Restore
```bash
git restore <file>             # Discard changes in working directory
git restore --staged <file>    # Unstage file (keep changes in working directory)
git reset HEAD~1               # Undo last commit (keep changes in working directory)
```

### 4.5 Stash Changes
Git stash lets you temporarily save your uncommitted changes.
```bash
git stash                           # Save both staged and unstaged changes.
git stash pop                       # Restore most recent stash
git stash list                      # View all stashes
git stash drop                      # Delete a stash
```

### 4.6 Commit vs Stash
**Commit** 
- Permanently saves changes to the repository.
- Records a snapshot of your project with a message.
- Changes are part of Git history and can be pushed to share with others.

**Stash**

- Temporarily saves changes without committing.
- Hides your work so you can switch branches or pull updates safely.
- Not part of Git history and only visible locally when applied.
- Useful for unfinished work you want to set aside.


## 5. Branches
A branch is a separate copy of your project where you can make changes safely. It lets you work on new features or fix bugs without affecting the main version of the code. Once complete, you merge it back into the main branch.


#### Common branches:
- `main` - the default branch of a git repository, which contains the latest stable version of the project (production-ready code)
- `feature/{feature-name}` — a branch for a specific task


#### Branch-related commands:
- **List branches:**
```bash
git branch                      # List local branches
git branch -r                   # List remote branches
git branch -a                   # List all (local & remote) branches
```

- **Switch branches:**
```bash
git checkout <branch-name>      # Switch to an existing branch
git switch <branch-name>        # Switch to an existing branch (Git 2.23+)
```

- **Create branches:**
```bash
git branch <branch-name>        # Create new branch locally (does NOT switch to it)
git checkout -b <branch-name>   # Create and switch to new branch
git switch -c <branch-name>     # Create and switch to a new branch (Git 2.23+)
```

- **Merge branches:**
```bash
git merge <branch-name>         # Merge the specified branch into the current branch
```

- **Delete branches**:
```bash
git branch -d <branch-name>   # Delete a local branch (only if it has been merged)
git branch -D <branch-name>   # Force delete a local branch (even if unmerged)
```
*Note: You cannot delete a branch that you are currently on. Switch to a different branch first before deleting.*


## 6. Remote Repositories
```bash
git fetch                           # Get updates from remote without merging
git pull                            # Fetch and merge changes from the current remote branch
git pull origin <branch>            # Fetch and merge changes from a specific remote branch
git push                            # Push your local commits to the current remote branch
git push origin <branch>            # Push your local commits to a specific remote branch
```

## 7. Pull Requests

### What is a Pull Request?

A pull request (PR) is a way to propose changes to a project. It allows you to:
- Review code before merging
- Discuss changes with team members
- Run automated tests
- Merge safely into main

### How to create a Pull Request on Github

1. Go to the repository on Github and select the "Pull requests" tab
2. Click "New Pull Request"
3. Choose your branch as the source (compare) and the main branch as the target (base)
4. Click "Create pull request"
5. Add title and description 
6. Request reviewers 
7. Click on "Create pull request" and wait for review 
8. Merge into the main branch when approved

### After Merge
```bash
git switch main                              # Switch to main branch
git pull                                     # Get merged changes
git branch -d <branch-name>                  # Delete local branch
git push origin --delete <branch-name>       # Delete remote branch
```

### Merge Conflicts
Merge conflicts occur when Git can’t decide how to merge conflicting changes, because a file is changed both in remote and in local version. Here's how to handle them:
```bash
git fetch origin                    # Get latest updates
git merge origin/main               # Attempt to merge
# Git will mark conflicting files
# Edit the conflicted files manually
# Look for markers: <<<<<<<, =======, >>>>>>>
git add <resolved-file>             # Stage resolved files
git commit -m "Resolve merge conflict"
```

##  8. `.gitignore` file
It's a common practice to create a `.gitignore` file in your repository root to exclude files from being tracked. Sοme examples are:
```bash
node_modules/
.env
__pycache__/
.vscode/
```

##  Typical Workflow Summary
1. Create or clone a repository 
2. Create a feature branch
3. Make changes to files 
4. Stage changes: `git add .`
5. Commit changes: `git commit -m "message"`
6. Push to remote: `git push origin main`
7. Create a Pull Request
8. Merge to main branch and delete feature branch