GIT COMMANDS AND SCENARIO ANSWERS

Text-only copyable guide



Replace words in <angle brackets> with your own values. Do not type the angle brackets.



============================================================================

1\. FIRST-TIME SETUP

============================================================================



git --version

\# Shows installed Git version.



git config --global user.name "Your Name"

git config --global user.email "you@example.com"

git config --global init.defaultBranch main

git config --list

\# Sets identity, default new-branch name, and displays configuration.



============================================================================

2\. CREATE OR COPY A REPOSITORY

============================================================================



git init

\# Start Git in the current project folder.



git clone https://github.com/<username>/<repository>.git

cd <repository>

\# Copy a remote repository locally.



git status

\# Check changed, staged, and untracked files.



============================================================================

3\. DAILY SAVE WORKFLOW

============================================================================



git status

git add <file>

git add .

git restore --staged <file>

git diff

git diff --staged

git commit -m "Add login form validation"

git commit -m "Fix navbar alignment on mobile"

git commit -m "Update README installation steps"



Good commit-message pattern:

<Verb> <what changed>

Examples: Add search filter, Fix API timeout, Remove unused CSS, Update project documentation.



============================================================================

4\. VIEW HISTORY AND CHANGES

============================================================================



git log

git log --oneline --graph --decorate --all

git show <commit-hash>

git diff

git diff --staged

git diff <branch1>..<branch2>

git blame -L 25,25 script.py

git reflog



============================================================================

5\. CONNECT TO GITHUB OR ANOTHER REMOTE

============================================================================



git remote -v

git remote add origin https://github.com/<username>/<repository>.git

git remote show origin

git remote set-url origin https://github.com/<username>/<new-repository>.git

git remote rename origin upstream

git remote remove origin



First push of a new repository:

git branch -M main

git push -u origin main



Push later commits:

git push

\# Or explicitly:

git push origin main



============================================================================

6\. DOWNLOAD REMOTE CHANGES

============================================================================



git fetch origin

\# Downloads remote information; does not merge it.



git fetch origin <branch-name>

git pull origin main

\# Fetches and merges remote main into the current local main branch.



git pull --rebase origin main

\# Fetches then replays your local commits on top of remote main.



git remote prune origin

git fetch --prune origin

\# Removes stale remote-tracking branch references.



============================================================================

7\. BRANCHES

============================================================================



git branch

git branch -a

git branch -r

git switch -c feature/search-filter

git switch feature/search-filter

git switch main

\# Older equivalent: git checkout -b <branch> and git checkout <branch>.



git push -u origin feature/search-filter

git branch -d feature/search-filter

git branch -D feature/experiment

git push origin --delete feature/search-filter

git branch --merged main

git branch --no-merged main



============================================================================

8\. MERGE A FEATURE INTO MAIN

============================================================================



git switch main

git pull --ff-only origin main

git merge feature/signup

git push origin main



If the merge is not ready to keep:

git merge --abort



============================================================================

9\. UPDATE A FEATURE BRANCH WITH MAIN

============================================================================



git switch main

git pull --ff-only origin main

git switch feature/ui-update

git merge main

\# Alternative, only if your team allows rebasing shared work:

git rebase main



After a rebase of a branch already pushed by you:

git push --force-with-lease origin feature/ui-update

\# Never use plain --force unless you fully understand the risk.



============================================================================

10\. MERGE-CONFLICT RESOLUTION

============================================================================



git status

\# Open each conflicted file. Choose or combine the content, then delete:

\# <<<<<<<

\# =======

\# >>>>>>>



git add <resolved-file>

git commit

git push



For a rebase conflict:

git add <resolved-file>

git rebase --continue



Cancel instead:

git merge --abort

git rebase --abort



============================================================================

11\. UNDO AND RECOVER

============================================================================



git restore <file>

\# Discard unstaged changes in one file.



git restore .

\# Discard all unstaged working-tree changes. Use carefully.



git restore --staged <file>

\# Unstage a file but keep its edits.



git commit --amend -m "Correct commit message"

\# Change the latest unpushed commit message.



git revert <commit-hash>

\# Safely undo a published commit by creating a new reversing commit.



git reset --soft HEAD\~1

\# Undo latest commit but keep changes staged.



git reset HEAD\~1

\# Undo latest commit but keep changes unstaged.



git reset --hard HEAD\~1

\# Deletes latest commit and its changes. Use only when the changes are truly unwanted.



git reflog

git switch -c feature-ui <commit-hash>

\# Recover a deleted branch from its commit hash.



============================================================================

12\. STASH TEMPORARY WORK

============================================================================



git stash push -m "WIP login form"

git stash list

git stash apply

git stash pop

git stash drop



============================================================================

13\. IGNORE FILES

============================================================================



Create a .gitignore file containing, for example:

\*.log

node\_modules/

.env

dist/



If a file is already tracked, ignoring it alone is not enough:

git rm --cached <file>

git commit -m "Stop tracking generated file"



============================================================================

14\. SENSITIVE FILE ACCIDENTALLY PUSHED

============================================================================



1\. Revoke or rotate the exposed API key/password immediately.

2\. Add the file to .gitignore.

3\. Remove it from current tracking:

&#x20;  git rm --cached <secret-file>

&#x20;  git commit -m "Remove exposed secret file"

&#x20;  git push origin main

4\. To remove it from all Git history, use git filter-repo (recommended):

&#x20;  git filter-repo --path <secret-file> --invert-paths

&#x20;  git push --force --all

&#x20;  git push --force --tags

5\. Tell collaborators to re-clone or carefully reset their copies.



============================================================================

15\. PATCHES

============================================================================



git format-patch -1 <commit-hash>

\# Creates one patch file from a commit.



git format-patch -3

\# Creates patches for the latest three commits.



git format-patch <base-commit>..HEAD

\# Creates patches for all commits after base commit.



git am <patch-file>.patch

\# Applies a patch made by git format-patch and preserves its commit message/history.



git apply <patch-file>.patch

\# Applies only the file changes; you must stage and commit afterwards.



git apply --check <patch-file>.patch

\# Checks whether the patch can apply cleanly.



============================================================================

16\. COLLABORATION WORKFLOW

============================================================================



git clone <shared-repository-url>

cd <repository>

git switch -c feature/your-feature

\# edit files

git add .

git commit -m "Add <feature description>"

git push -u origin feature/your-feature

\# Create a Pull Request on GitHub. Review, merge, then update local main:

git switch main

git pull --ff-only origin main



============================================================================

17\. FORK WORKFLOW (PUBLIC PROJECT)

============================================================================



1\. Fork the project on GitHub.

2\. Clone your fork:

&#x20;  git clone https://github.com/<your-user>/<repository>.git

3\. Add original project as upstream:

&#x20;  git remote add upstream https://github.com/<original-owner>/<repository>.git

4\. Work on a branch, commit, and push:

&#x20;  git switch -c feature/contribution

&#x20;  git add .

&#x20;  git commit -m "Fix <description>"

&#x20;  git push -u origin feature/contribution

5\. Open a Pull Request from your fork to the original repository.

6\. Keep your fork current:

&#x20;  git fetch upstream

&#x20;  git switch main

&#x20;  git merge upstream/main

&#x20;  git push origin main



============================================================================

18\. SCENARIO ANSWERS: BASIC GIT

============================================================================



1\. Discard unstaged changes in file1.txt:

&#x20;  git restore file1.txt



2\. Remove file1.txt from staging without losing edits:

&#x20;  git restore --staged file1.txt



3\. Correct the latest unpushed commit message:

&#x20;  git commit --amend -m "Correct commit message"



4\. Readable current-branch history:

&#x20;  git log --oneline



5\. Set global name and email:

&#x20;  git config --global user.name "Your Name"

&#x20;  git config --global user.email "you@example.com"



6\. View unstaged edits:

&#x20;  git diff



7\. Switch to feature/login:

&#x20;  git switch feature/login



8\. Recover deleted feature-ui branch:

&#x20;  git reflog

&#x20;  git switch -c feature-ui <commit-hash>



9\. Upload local commits:

&#x20;  git push origin <current-branch>



10\. Download changes without merging:

&#x20;   git fetch origin



11\. Start feature/search-filter from main:

&#x20;   git switch main

&#x20;   git switch -c feature/search-filter



12\. Remove an API key file from history:

&#x20;   Rotate the key, then use git filter-repo --path <secret-file> --invert-paths

&#x20;   Push rewritten history only after coordinating with the team.



13\. List local and remote branches:

&#x20;   git branch -a



14\. Merge feature/signup into main:

&#x20;   git switch main

&#x20;   git merge feature/signup



15\. Resolve conflict in app.js:

&#x20;   Edit app.js; remove conflict markers; keep correct code; then:

&#x20;   git add app.js

&#x20;   git commit



16\. Ignore log files and node\_modules:

&#x20;   Put these lines in .gitignore:

&#x20;   \*.log

&#x20;   node\_modules/



17\. Find who changed line 25 in script.py:

&#x20;   git blame -L 25,25 script.py



18\. Save unfinished work before switching branches:

&#x20;   git stash push -m "WIP"

&#x20;   git switch <other-branch>



19\. Restore stashed changes:

&#x20;   git stash pop



20\. Delete feature/test locally:

&#x20;   git branch -d feature/test



21\. Safely delete merged feature-ui:

&#x20;   git branch -d feature-ui



22\. Force-delete unmerged feature-experiment:

&#x20;   git branch -D feature-experiment



23\. Before deleting feature-ui, ensure you are not currently on it:

&#x20;   git switch main

&#x20;   git branch -d feature-ui



24\. Check whether bugfix-footer was merged, then delete safely:

&#x20;   git branch --merged main

&#x20;   git branch -d bugfix-footer



25\. Delete several merged local branches:

&#x20;   git branch -d feature-a feature-b feature-c



============================================================================

19\. SCENARIO ANSWERS: REMOTE REPOSITORIES

============================================================================



1\. Clone remote repository:

&#x20;  git clone <repository-url>

2\. View connected remotes:

&#x20;  git remote -v

3\. Add a remote:

&#x20;  git remote add origin <repository-url>

4\. Remove a remote:

&#x20;  git remote remove origin

5\. Rename a remote:

&#x20;  git remote rename origin upstream

6\. Fetch without merging:

&#x20;  git fetch origin

7\. Pull and merge latest main:

&#x20;  git pull origin main

8\. Push local commits:

&#x20;  git push origin main

9\. First push and set upstream:

&#x20;  git push -u origin <branch-name>

10\. Change remote URL:

&#x20;   git remote set-url origin <new-repository-url>

11\. List remote branches:

&#x20;   git branch -r

12\. Remove stale deleted remote branches:

&#x20;   git fetch --prune origin

13\. Fetch one remote branch:

&#x20;   git fetch origin <branch-name>

14\. Detailed remote information:

&#x20;   git remote show origin

15\. Rebase current branch on remote main:

&#x20;   git fetch origin

&#x20;   git rebase origin/main



============================================================================

20\. WEEK 3 COLLABORATION SCENARIO: feature/ui-update AND PATCH

============================================================================



Bring local main up to date before merging it into the feature branch:

git switch main

git pull --ff-only origin main



Update feature/ui-update with latest main:

git switch feature/ui-update

git merge main

\# Or, if the team uses rebase:

\# git rebase main



Push feature branch again:

git push origin feature/ui-update



If push is rejected because the remote branch changed:

git pull --rebase origin feature/ui-update

\# Resolve any conflicts, then:

git add <resolved-file>

git rebase --continue

git push origin feature/ui-update



Apply a teammate patch while preserving its commit history:

git switch feature/ui-update

git am <teammate-fix>.patch

\# If it conflicts: resolve files, git add <file>, then git am --continue.

\# To cancel: git am --abort.



Test, merge feature branch into main, and push:

git switch main

git pull --ff-only origin main

git merge feature/ui-update

git push origin main



============================================================================

21\. QUICK SAFETY RULES

============================================================================



\- Run git status before and after important commands.

\- Use a feature branch; do not directly edit shared main unless your team requires it.

\- Pull or fetch before starting work and before merging.

\- Prefer git revert for commits already pushed to a shared repository.

\- Do not commit API keys, passwords, .env files, build folders, or node\_modules.

\- Prefer git push --force-with-lease over git push --force when a force-push is unavoidable.

\- Resolve conflicts in the file, remove all conflict markers, test, then stage and commit.GIT COMMANDS AND SCENARIO ANSWERS

Text-only copyable guide



Replace words in <angle brackets> with your own values. Do not type the angle brackets.



============================================================================

1\. FIRST-TIME SETUP

============================================================================



git --version

\# Shows installed Git version.



git config --global user.name "Your Name"

git config --global user.email "you@example.com"

git config --global init.defaultBranch main

git config --list

\# Sets identity, default new-branch name, and displays configuration.



============================================================================

2\. CREATE OR COPY A REPOSITORY

============================================================================



git init

\# Start Git in the current project folder.



git clone https://github.com/<username>/<repository>.git

cd <repository>

\# Copy a remote repository locally.



git status

\# Check changed, staged, and untracked files.



============================================================================

3\. DAILY SAVE WORKFLOW

============================================================================



git status

git add <file>

git add .

git restore --staged <file>

git diff

git diff --staged

git commit -m "Add login form validation"

git commit -m "Fix navbar alignment on mobile"

git commit -m "Update README installation steps"



Good commit-message pattern:

<Verb> <what changed>

Examples: Add search filter, Fix API timeout, Remove unused CSS, Update project documentation.



============================================================================

4\. VIEW HISTORY AND CHANGES

============================================================================



git log

git log --oneline --graph --decorate --all

git show <commit-hash>

git diff

git diff --staged

git diff <branch1>..<branch2>

git blame -L 25,25 script.py

git reflog



============================================================================

5\. CONNECT TO GITHUB OR ANOTHER REMOTE

============================================================================



git remote -v

git remote add origin https://github.com/<username>/<repository>.git

git remote show origin

git remote set-url origin https://github.com/<username>/<new-repository>.git

git remote rename origin upstream

git remote remove origin



First push of a new repository:

git branch -M main

git push -u origin main



Push later commits:

git push

\# Or explicitly:

git push origin main



============================================================================

6\. DOWNLOAD REMOTE CHANGES

============================================================================



git fetch origin

\# Downloads remote information; does not merge it.



git fetch origin <branch-name>

git pull origin main

\# Fetches and merges remote main into the current local main branch.



git pull --rebase origin main

\# Fetches then replays your local commits on top of remote main.



git remote prune origin

git fetch --prune origin

\# Removes stale remote-tracking branch references.



============================================================================

7\. BRANCHES

============================================================================



git branch

git branch -a

git branch -r

git switch -c feature/search-filter

git switch feature/search-filter

git switch main

\# Older equivalent: git checkout -b <branch> and git checkout <branch>.



git push -u origin feature/search-filter

git branch -d feature/search-filter

git branch -D feature/experiment

git push origin --delete feature/search-filter

git branch --merged main

git branch --no-merged main



============================================================================

8\. MERGE A FEATURE INTO MAIN

============================================================================



git switch main

git pull --ff-only origin main

git merge feature/signup

git push origin main



If the merge is not ready to keep:

git merge --abort



============================================================================

9\. UPDATE A FEATURE BRANCH WITH MAIN

============================================================================



git switch main

git pull --ff-only origin main

git switch feature/ui-update

git merge main

\# Alternative, only if your team allows rebasing shared work:

git rebase main



After a rebase of a branch already pushed by you:

git push --force-with-lease origin feature/ui-update

\# Never use plain --force unless you fully understand the risk.



============================================================================

10\. MERGE-CONFLICT RESOLUTION

============================================================================



git status

\# Open each conflicted file. Choose or combine the content, then delete:

\# <<<<<<<

\# =======

\# >>>>>>>



git add <resolved-file>

git commit

git push



For a rebase conflict:

git add <resolved-file>

git rebase --continue



Cancel instead:

git merge --abort

git rebase --abort



============================================================================

11\. UNDO AND RECOVER

============================================================================



git restore <file>

\# Discard unstaged changes in one file.



git restore .

\# Discard all unstaged working-tree changes. Use carefully.



git restore --staged <file>

\# Unstage a file but keep its edits.



git commit --amend -m "Correct commit message"

\# Change the latest unpushed commit message.



git revert <commit-hash>

\# Safely undo a published commit by creating a new reversing commit.



git reset --soft HEAD\~1

\# Undo latest commit but keep changes staged.



git reset HEAD\~1

\# Undo latest commit but keep changes unstaged.



git reset --hard HEAD\~1

\# Deletes latest commit and its changes. Use only when the changes are truly unwanted.



git reflog

git switch -c feature-ui <commit-hash>

\# Recover a deleted branch from its commit hash.



============================================================================

12\. STASH TEMPORARY WORK

============================================================================



git stash push -m "WIP login form"

git stash list

git stash apply

git stash pop

git stash drop



============================================================================

13\. IGNORE FILES

============================================================================



Create a .gitignore file containing, for example:

\*.log

node\_modules/

.env

dist/



If a file is already tracked, ignoring it alone is not enough:

git rm --cached <file>

git commit -m "Stop tracking generated file"



============================================================================

14\. SENSITIVE FILE ACCIDENTALLY PUSHED

============================================================================



1\. Revoke or rotate the exposed API key/password immediately.

2\. Add the file to .gitignore.

3\. Remove it from current tracking:

&#x20;  git rm --cached <secret-file>

&#x20;  git commit -m "Remove exposed secret file"

&#x20;  git push origin main

4\. To remove it from all Git history, use git filter-repo (recommended):

&#x20;  git filter-repo --path <secret-file> --invert-paths

&#x20;  git push --force --all

&#x20;  git push --force --tags

5\. Tell collaborators to re-clone or carefully reset their copies.



============================================================================

15\. PATCHES

============================================================================



git format-patch -1 <commit-hash>

\# Creates one patch file from a commit.



git format-patch -3

\# Creates patches for the latest three commits.



git format-patch <base-commit>..HEAD

\# Creates patches for all commits after base commit.



git am <patch-file>.patch

\# Applies a patch made by git format-patch and preserves its commit message/history.



git apply <patch-file>.patch

\# Applies only the file changes; you must stage and commit afterwards.



git apply --check <patch-file>.patch

\# Checks whether the patch can apply cleanly.



============================================================================

16\. COLLABORATION WORKFLOW

============================================================================



git clone <shared-repository-url>

cd <repository>

git switch -c feature/your-feature

\# edit files

git add .

git commit -m "Add <feature description>"

git push -u origin feature/your-feature

\# Create a Pull Request on GitHub. Review, merge, then update local main:

git switch main

git pull --ff-only origin main



============================================================================

17\. FORK WORKFLOW (PUBLIC PROJECT)

============================================================================



1\. Fork the project on GitHub.

2\. Clone your fork:

&#x20;  git clone https://github.com/<your-user>/<repository>.git

3\. Add original project as upstream:

&#x20;  git remote add upstream https://github.com/<original-owner>/<repository>.git

4\. Work on a branch, commit, and push:

&#x20;  git switch -c feature/contribution

&#x20;  git add .

&#x20;  git commit -m "Fix <description>"

&#x20;  git push -u origin feature/contribution

5\. Open a Pull Request from your fork to the original repository.

6\. Keep your fork current:

&#x20;  git fetch upstream

&#x20;  git switch main

&#x20;  git merge upstream/main

&#x20;  git push origin main



============================================================================

18\. SCENARIO ANSWERS: BASIC GIT

============================================================================



1\. Discard unstaged changes in file1.txt:

&#x20;  git restore file1.txt



2\. Remove file1.txt from staging without losing edits:

&#x20;  git restore --staged file1.txt



3\. Correct the latest unpushed commit message:

&#x20;  git commit --amend -m "Correct commit message"



4\. Readable current-branch history:

&#x20;  git log --oneline



5\. Set global name and email:

&#x20;  git config --global user.name "Your Name"

&#x20;  git config --global user.email "you@example.com"



6\. View unstaged edits:

&#x20;  git diff



7\. Switch to feature/login:

&#x20;  git switch feature/login



8\. Recover deleted feature-ui branch:

&#x20;  git reflog

&#x20;  git switch -c feature-ui <commit-hash>



9\. Upload local commits:

&#x20;  git push origin <current-branch>



10\. Download changes without merging:

&#x20;   git fetch origin



11\. Start feature/search-filter from main:

&#x20;   git switch main

&#x20;   git switch -c feature/search-filter



12\. Remove an API key file from history:

&#x20;   Rotate the key, then use git filter-repo --path <secret-file> --invert-paths

&#x20;   Push rewritten history only after coordinating with the team.



13\. List local and remote branches:

&#x20;   git branch -a



14\. Merge feature/signup into main:

&#x20;   git switch main

&#x20;   git merge feature/signup



15\. Resolve conflict in app.js:

&#x20;   Edit app.js; remove conflict markers; keep correct code; then:

&#x20;   git add app.js

&#x20;   git commit



16\. Ignore log files and node\_modules:

&#x20;   Put these lines in .gitignore:

&#x20;   \*.log

&#x20;   node\_modules/



17\. Find who changed line 25 in script.py:

&#x20;   git blame -L 25,25 script.py



18\. Save unfinished work before switching branches:

&#x20;   git stash push -m "WIP"

&#x20;   git switch <other-branch>



19\. Restore stashed changes:

&#x20;   git stash pop



20\. Delete feature/test locally:

&#x20;   git branch -d feature/test



21\. Safely delete merged feature-ui:

&#x20;   git branch -d feature-ui



22\. Force-delete unmerged feature-experiment:

&#x20;   git branch -D feature-experiment



23\. Before deleting feature-ui, ensure you are not currently on it:

&#x20;   git switch main

&#x20;   git branch -d feature-ui



24\. Check whether bugfix-footer was merged, then delete safely:

&#x20;   git branch --merged main

&#x20;   git branch -d bugfix-footer



25\. Delete several merged local branches:

&#x20;   git branch -d feature-a feature-b feature-c



============================================================================

19\. SCENARIO ANSWERS: REMOTE REPOSITORIES

============================================================================



1\. Clone remote repository:

&#x20;  git clone <repository-url>

2\. View connected remotes:

&#x20;  git remote -v

3\. Add a remote:

&#x20;  git remote add origin <repository-url>

4\. Remove a remote:

&#x20;  git remote remove origin

5\. Rename a remote:

&#x20;  git remote rename origin upstream

6\. Fetch without merging:

&#x20;  git fetch origin

7\. Pull and merge latest main:

&#x20;  git pull origin main

8\. Push local commits:

&#x20;  git push origin main

9\. First push and set upstream:

&#x20;  git push -u origin <branch-name>

10\. Change remote URL:

&#x20;   git remote set-url origin <new-repository-url>

11\. List remote branches:

&#x20;   git branch -r

12\. Remove stale deleted remote branches:

&#x20;   git fetch --prune origin

13\. Fetch one remote branch:

&#x20;   git fetch origin <branch-name>

14\. Detailed remote information:

&#x20;   git remote show origin

15\. Rebase current branch on remote main:

&#x20;   git fetch origin

&#x20;   git rebase origin/main



============================================================================

20\. WEEK 3 COLLABORATION SCENARIO: feature/ui-update AND PATCH

============================================================================



Bring local main up to date before merging it into the feature branch:

git switch main

git pull --ff-only origin main



Update feature/ui-update with latest main:

git switch feature/ui-update

git merge main

\# Or, if the team uses rebase:

\# git rebase main



Push feature branch again:

git push origin feature/ui-update



If push is rejected because the remote branch changed:

git pull --rebase origin feature/ui-update

\# Resolve any conflicts, then:

git add <resolved-file>

git rebase --continue

git push origin feature/ui-update



Apply a teammate patch while preserving its commit history:

git switch feature/ui-update

git am <teammate-fix>.patch

\# If it conflicts: resolve files, git add <file>, then git am --continue.

\# To cancel: git am --abort.



Test, merge feature branch into main, and push:

git switch main

git pull --ff-only origin main

git merge feature/ui-update

git push origin main



============================================================================

21\. QUICK SAFETY RULES

============================================================================



\- Run git status before and after important commands.

\- Use a feature branch; do not directly edit shared main unless your team requires it.

\- Pull or fetch before starting work and before merging.

\- Prefer git revert for commits already pushed to a shared repository.

\- Do not commit API keys, passwords, .env files, build folders, or node\_modules.

\- Prefer git push --force-with-lease over git push --force when a force-push is unavoidable.

\- Resolve conflicts in the file, remove all conflict markers, test, then stage and commit.

