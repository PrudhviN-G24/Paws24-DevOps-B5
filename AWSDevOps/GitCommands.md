### Git Commands Cheatsheet

#### **1. Setting up a Repository**

- **`git init`**: 🚫📂 Initialize a new Git repository.
  ```bash
  git init
  ```
- **`git clone`**: 🔗 Clone an existing repository.
  ```bash
  git clone <repository-url>
  git clone <repository-url> <directory>
  ```

#### **2. Checking Repository Status**

- **`git status`**: 🔍 Show the working directory and staging area status.
  ```bash
  git status
  ```

#### **3. Tracking and Staging Changes**

- **`git add`**: ➕ Add changes to the staging area.
  ```bash
  git add <file>
  git add .  # Add all changes
  git add *.txt  # Add all .txt files
  ```

#### **4. Committing Changes**

- **`git commit`**: 🖋️ Commit staged changes with a message.
  ```bash
  git commit -m "Commit message"
  git commit -a -m "Commit message"  # Add and commit in one step
  ```
- **`git commit --amend`**: ✏️ Modify the last commit.
  ```bash
  git commit --amend -m "Updated commit message"
  ```

#### **5. Branching**

- **`git branch`**: 🔄 List, create, or delete branches.
  ```bash
  git branch  # List branches
  git branch <branch-name>  # Create a new branch
  git branch -d <branch-name>  # Delete a branch
  git branch -m <new-name>  # Rename the current branch
  ```
- **`git switch`**: 🎩 Switch between branches.
  ```bash
  git switch <branch-name>
  git switch -c <new-branch-name>  # Create and switch to a new branch
  ```
- **`git checkout`**: (Deprecated in favor of `git switch`) 📝 Switch branches or restore files.
  ```bash
  git checkout <branch-name>
  git checkout <commit-hash>  # Check out a specific commit
  ```

#### **6. Merging and Rebasing**

- **`git merge`**: ➕📝 Merge a branch into the current branch.
  ```bash
  git merge <branch-name>
  ```
  **Handling Merge Conflicts**: If conflicts occur, Git will notify you about the files with conflicts. Open the files, resolve conflicts manually, and then:
  ```bash
  git add <file-with-conflict>
  git commit -m "Resolve merge conflict"
  ```
- **`git rebase`**: 🏛️ Reapply commits on top of another branch.
  ```bash
  git rebase <branch-name>
  ```

#### **7. Remote Repositories**

- **`git remote`**: 🌐 Manage remote repositories.
  ```bash
  git remote add <name> <url>
  git remote -v  # List remote URLs
  git remote remove <name>
  ```
- **`git push`**: 💨 Push changes to a remote repository.
  ```bash
  git push
  git push <remote> <branch>
  git push -u <remote> <branch>  # Set upstream branch
  ```
- **`git pull`**: 📥 Fetch and merge changes from a remote repository.
  ```bash
  git pull <remote> <branch>
  ```
- **`git fetch`**: 🍎 Fetch changes from a remote repository without merging.
  ```bash
  git fetch
  ```

#### **8. Undoing Changes**

- **`git restore`**: ♻️ Discard changes in the working directory.
  ```bash
  git restore <file>
  git restore --staged <file>  # Unstage a file
  ```
- **`git reset`**: ⚡ Undo commits or unstage files.
  ```bash
  git reset HEAD~1  # Remove the last commit
  git reset <file>  # Unstage a file
  git reset --hard  # Discard all changes
  ```
- **`git revert`**: ↩ Create a new commit that undoes a previous commit.
  ```bash
  git revert <commit-hash>
  ```

#### **9. Stashing**

- **`git stash`**: 🌐 Save changes temporarily.
  ```bash
  git stash
  git stash push -m "Message"
  ```
- **`git stash pop`**: 🔄 Apply stashed changes and remove them from stash.
  ```bash
  git stash pop
  ```
- **`git stash list`**: 🔍 List all stashes.
  ```bash
  git stash list
  ```

#### **10. Viewing Logs and History**

- **`git log`**: 🔬 Show commit history.
  ```bash
  git log
  git log --oneline  # Compact format
  git log --graph --all --decorate  # Visualize branches and merges
  ```
- **`git diff`**: 🎨 Show changes between commits, branches, or working directory.
  ```bash
  git diff
  git diff <commit-hash>
  git diff <branch1> <branch2>
  ```

#### **11. Tags**

- **`git tag`**: 🌟 Create and manage tags.
  ```bash
  git tag <tag-name>
  git tag -a <tag-name> -m "Message"  # Annotated tag
  git push origin <tag-name>
  ```

#### **12. Debugging and Finding Issues**

- **`git bisect`**: ♾ Perform a binary search to find a commit that introduced a bug.
  ```bash
  git bisect start
  git bisect bad  # Mark current commit as bad
  git bisect good <commit-hash>  # Mark a known good commit
  ```
- **`git blame`**: 👀 Show who modified each line of a file.
  ```bash
  git blame <file>
  ```

#### **13. Ignoring Files**

- **`.gitignore`**: 🚿 Specify files or directories to ignore.
  ```text
  # Example .gitignore file
  node_modules/
  *.log
  build/
  ```

#### **14. Archiving and Bundling**

- **`git archive`**: 📂 Create a tar or zip archive of the repository.
  ```bash
  git archive --format=zip HEAD > archive.zip
  ```

#### **15. Configurations**

- **`git config`**: 🔧 Set global or local configurations.
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your.email@example.com"
  git config --list  # View all configurations
  ```

#### **Pull Requests**

- **What is a Pull Request (PR)?**: A PR is a way to propose changes in a repository and collaborate before merging them into the main branch. Typically used in platforms like GitHub, GitLab, or Bitbucket.

- **Steps to Create a Pull Request**:
  1. Push your branch to the remote repository:
     ```bash
     git push origin <branch-name>
     ```
  2. Open the repository on the platform (e.g., GitHub).
  3. Click on "New Pull Request" and select your branch and the base branch.
  4. Add a title, description, and optionally request reviews.

- **Merging a Pull Request**:
  Once approved, merge the PR via the platform, or locally by:
  ```bash
  git checkout main
  git pull origin main  # Ensure main is up-to-date
  git merge <branch-name>
  ```

#### **Examples for `git rebase`, `git cherry-pick`, `git fetch`, `git pull`, and `git log`**

- **`git rebase`**:
  Reapply commits on top of another branch.
  ```bash
  # Rebase feature branch on top of main
  git checkout feature-branch
  git rebase main
  ```
  Example scenario: If your feature branch is behind the `main` branch, use rebase to bring your changes on top of the latest `main` branch commits, creating a cleaner project history.

- **`git cherry-pick`**:
  Apply a specific commit from another branch.
  ```bash
  # Cherry-pick a commit from main into the current branch
  git cherry-pick <commit-hash>
  ```
  Example scenario: If a bug fix was made in the `main` branch and you need it in your `feature-branch`, cherry-pick the specific commit.

- **`git fetch` vs `git pull`**:
  - **`git fetch`**: Fetch updates from the remote repository without merging.
    ```bash
    git fetch origin
    ```
    Example scenario: See what changes are available in the remote repository without affecting your local branch.

  - **`git pull`**: Fetch and merge updates from the remote repository.
    ```bash
    git pull origin main
    ```
    Example scenario: Use pull to bring changes from the remote repository into your local branch, combining fetch and merge in one step.

- **`git log`**:
  View commit history.
  ```bash
  git log  # Full log
  git log --oneline  # Compact format
  git log --graph --all --decorate  # Visualize branches and merges
  ```
  Example scenario: Use `git log` to review the commit history, identify changes, or explore past states of the project.

