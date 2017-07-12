# Git Cheat Sheet

## Legend
`ref` &nbsp;&nbsp;&nbsp;&nbsp; `<hash|tag|branch|HEAD|reflog|remote/branch>`  
examples: `origin/master`, `HEAD~2`, `master@{3}`, `@{-1}`, `HEAD^`  
`<xyz>` &nbsp;&nbsp;&nbsp;&nbsp; name for particular file or string or branch etc.  
`(xyz)` &nbsp;&nbsp;&nbsp;&nbsp; optional parmeter  

## Help
`git help`, `git xyz --help`, `man git-xyz`

## Local Work

### Get Infos

`gitk --all` &nbsp;&nbsp;&nbsp;&nbsp; visual git log with search

`git log ref` &nbsp;&nbsp;&nbsp;&nbsp; log history until `ref`  
&nbsp;&nbsp;&nbsp;&nbsp; `-i` &nbsp;&nbsp;&nbsp;&nbsp; case insensitive  
&nbsp;&nbsp;&nbsp;&nbsp; `--all` &nbsp;&nbsp;&nbsp;&nbsp; all branches  
&nbsp;&nbsp;&nbsp;&nbsp; `-p` &nbsp;&nbsp;&nbsp;&nbsp; show diff  
&nbsp;&nbsp;&nbsp;&nbsp; `-2` &nbsp;&nbsp;&nbsp;&nbsp; only last 2 (n) commits  
`git log ..ref` &nbsp;&nbsp;&nbsp;&nbsp; same as `log HEAD..ref`. Commits in `ref` that are not in current branch (unmerged)  
`git log ref..` &nbsp;&nbsp;&nbsp;&nbsp; same as `log ref..HEAD`. Commits in current branch that are not in `ref`  
`git log ref1..ref2` &nbsp;&nbsp;&nbsp;&nbsp; commits in `ref2` that are not in `ref1`  
`git log ref2 ref3 ^ref1` &nbsp;&nbsp;&nbsp;&nbsp; commits in `ref2` and `ref3` that are not in `ref1`  
`git log ref2 ref3 --not ref1` &nbsp;&nbsp;&nbsp;&nbsp; commits in `ref2` and `ref3` that are not in `ref1`  
`git log --left-right ref1...ref2` &nbsp;&nbsp;&nbsp;&nbsp; commits from `ref1` and `ref2` UNTIL the common ancestor. Commits only in either one of the branches  
`git log --cherry ref1...ref2` &nbsp;&nbsp;&nbsp;&nbsp; commits in `ref2` that are not in `ref1` AND are not patches or cherry-picks  
`git log <path>` &nbsp;&nbsp;&nbsp;&nbsp; log changes only for that path  

`git log -G<regex>` &nbsp;&nbsp;&nbsp;&nbsp; log history with changes that match regex. Use `-p` to see changes  
`git log -S'<string>'` &nbsp;&nbsp;&nbsp;&nbsp; log history with changes that match string. Use `-p` to see changes  
`git log -L '<start>','<end>':<file>` &nbsp;&nbsp;&nbsp;&nbsp; show changes in file for certain area. start, end can be line numbers, /regexp/, +-offset  
`git log -L :<funcName>:<file>` &nbsp;&nbsp;&nbsp;&nbsp; show changes for function, class, object  

`git log --grep='string'` &nbsp;&nbsp;&nbsp;&nbsp; search log messages  

`git log --follow <file>` &nbsp;&nbsp;&nbsp;&nbsp; log history of file (`--follow` = beyond renaming)  
`git log --patch <file>` &nbsp;&nbsp;&nbsp;&nbsp; diff history of file  
`git blame <file>` &nbsp;&nbsp;&nbsp;&nbsp; latest commit for each line  

`git reflog` &nbsp;&nbsp;&nbsp;&nbsp; reflog of `HEAD`  
&nbsp;&nbsp;&nbsp;&nbsp; `git reflog <branch|tag>` &nbsp;&nbsp;&nbsp;&nbsp; reflog of branch or tag  
`git log -g <branch|tag>` &nbsp;&nbsp;&nbsp;&nbsp; show reflog history as commit log (`HEAD` is default)  

`git show ref` &nbsp;&nbsp;&nbsp;&nbsp; show commit changes  
&nbsp;&nbsp;&nbsp;&nbsp; `--name-only` &nbsp;&nbsp;&nbsp;&nbsp; show only changed files  
&nbsp;&nbsp;&nbsp;&nbsp; `--word-diff=color` &nbsp;&nbsp;&nbsp;&nbsp; show changes inline with red/green colors for removed/added words  

`git status` &nbsp;&nbsp;&nbsp;&nbsp; show current working dir status  
&nbsp;&nbsp;&nbsp;&nbsp; `--short` &nbsp;&nbsp;&nbsp;&nbsp; abbreviated version of git status  

`git diff ref` &nbsp;&nbsp;&nbsp;&nbsp; From commit to working dir  
&nbsp;&nbsp;&nbsp;&nbsp; `--word-diff=color` &nbsp;&nbsp;&nbsp;&nbsp; show changes inline with red/green colors for removed/added words  
`git diff ref1..ref2` &nbsp;&nbsp;&nbsp;&nbsp; `ref1` older commit  
`git diff branch1 branch2` &nbsp;&nbsp;&nbsp;&nbsp; diff between two branches  
`git diff ...refFromOtherBranch` &nbsp;&nbsp;&nbsp;&nbsp; diff from common ancestor to `HEAD`  
`git diff ref1:file..ref2:file` &nbsp;&nbsp;&nbsp;&nbsp; diff in file between 2 commits  
`git diff HEAD` &nbsp;&nbsp;&nbsp;&nbsp; staged & unstaged changes  
`git diff` &nbsp;&nbsp;&nbsp;&nbsp; unstaged changes. Show merge conflicts  
`git diff --staged` or `--cached` &nbsp;&nbsp;&nbsp;&nbsp; staged changes  
&nbsp;&nbsp;&nbsp;&nbsp; `--word-diff` &nbsp;&nbsp;&nbsp;&nbsp; show inline changes, instead whole line as change  
&nbsp;&nbsp;&nbsp;&nbsp; `--check` &nbsp;&nbsp;&nbsp;&nbsp; show whitespace errors  

`git grep <'text'|regext>` &nbsp;&nbsp;&nbsp;&nbsp; search in codebase and all branches  
&nbsp;&nbsp;&nbsp;&nbsp; `-n -w -i` &nbsp;&nbsp;&nbsp;&nbsp; show line numbers, match only with word boundary, ignore case  
&nbsp;&nbsp;&nbsp;&nbsp; `--heading --break` &nbsp;&nbsp;&nbsp;&nbsp; show filename above matches, print empty line between matches of different files  
&nbsp;&nbsp;&nbsp;&nbsp; `-e <pattern> --and -e <...>` &nbsp;&nbsp;&nbsp;&nbsp; search with multiple regexes `--and` `--or` `--not`  
&nbsp;&nbsp;&nbsp;&nbsp; `--count` &nbsp;&nbsp;&nbsp;&nbsp; show summary of files and number occurences  

`git shortlog -nes` &nbsp;&nbsp;&nbsp;&nbsp; commit statistic by user with total number commits  

`git describe ref` &nbsp;&nbsp;&nbsp;&nbsp; describe commit by referencing most recent tag from `ref`. ie. v1.0.0-12-fe34da  

### Edit

`git gui` &nbsp;&nbsp;&nbsp;&nbsp; gui for staging & commiting  

`git add -u` &nbsp;&nbsp;&nbsp;&nbsp; add all tracked files (ignore untracked)  
`git add -i` &nbsp;&nbsp;&nbsp;&nbsp; stage interactively  
`git add -p` &nbsp;&nbsp;&nbsp;&nbsp; interactively select hunks to add  

`git rm <file>` &nbsp;&nbsp;&nbsp;&nbsp; stage deleted file(s) (escape * i.e.: .eslint\*)  
&nbsp;&nbsp;&nbsp;&nbsp; `--cached` &nbsp;&nbsp;&nbsp;&nbsp; remove file from tracking, but keep in file system  

`git mv <fileOld> <fileNew>` &nbsp;&nbsp;&nbsp;&nbsp; move or rename file  

`git reset <file|path>` &nbsp;&nbsp;&nbsp;&nbsp; unstage changes (only for files in path)  
`git reset ref` &nbsp;&nbsp;&nbsp;&nbsp; Move branch to that commit. Same as `--mixed`. Put resetted changes in workdir  
&nbsp;&nbsp;&nbsp;&nbsp; `--soft` &nbsp;&nbsp;&nbsp;&nbsp; Put resetted changes in Index/Staging Area. Can be used to squash commits  
&nbsp;&nbsp;&nbsp;&nbsp; `--hard` &nbsp;&nbsp;&nbsp;&nbsp; delete all resetted changes  
`git reset --hard ref` &nbsp;&nbsp;&nbsp;&nbsp; move branch to that commit  
`git reset -p` &nbsp;&nbsp;&nbsp;&nbsp; Interactively select hunks to unstage  

`git reset ref <file|path>` &nbsp;&nbsp;&nbsp;&nbsp; revert changes for specific file or folder, stage them. Keep changes in workdir  
`git checkout ref <file|path>` &nbsp;&nbsp;&nbsp;&nbsp; revert changes for specific file or folder, stage them. Overwrite changes in workdir  

`git clean -fd` &nbsp;&nbsp;&nbsp;&nbsp; delete untracked files  
&nbsp;&nbsp;&nbsp;&nbsp; `-f` &nbsp;&nbsp;&nbsp;&nbsp; force  
&nbsp;&nbsp;&nbsp;&nbsp; `-d` &nbsp;&nbsp;&nbsp;&nbsp; include directories  
&nbsp;&nbsp;&nbsp;&nbsp; `-n` &nbsp;&nbsp;&nbsp;&nbsp; shows what would be cleaned (-ndX)  
&nbsp;&nbsp;&nbsp;&nbsp; `-x` &nbsp;&nbsp;&nbsp;&nbsp; delete also ignored files  
&nbsp;&nbsp;&nbsp;&nbsp; `-X` &nbsp;&nbsp;&nbsp;&nbsp; delete only ignored files  
&nbsp;&nbsp;&nbsp;&nbsp; `-i` &nbsp;&nbsp;&nbsp;&nbsp; interactive mode  

`git stash` &nbsp;&nbsp;&nbsp;&nbsp; put local changes on stash stack  
&nbsp;&nbsp;&nbsp;&nbsp; `--keep-index` &nbsp;&nbsp;&nbsp;&nbsp; don't stash staged changes  
&nbsp;&nbsp;&nbsp;&nbsp; `--include-untracked` &nbsp;&nbsp;&nbsp;&nbsp; stash new files  
&nbsp;&nbsp;&nbsp;&nbsp; `-u` &nbsp;&nbsp;&nbsp;&nbsp; stash new files (same as --include-untracked)  
&nbsp;&nbsp;&nbsp;&nbsp; `-p` &nbsp;&nbsp;&nbsp;&nbsp; interactively select hunks to stash  
`git stash`  
&nbsp;&nbsp;&nbsp;&nbsp; `list` &nbsp;&nbsp;&nbsp;&nbsp; show list of stashed commits  
&nbsp;&nbsp;&nbsp;&nbsp; `show (stash)` &nbsp;&nbsp;&nbsp;&nbsp; show changes in last (or referenced) stash  
&nbsp;&nbsp;&nbsp;&nbsp; `drop (stash)` &nbsp;&nbsp;&nbsp;&nbsp; delete last (or referenced) stash  
&nbsp;&nbsp;&nbsp;&nbsp; `pop (stash)` &nbsp;&nbsp;&nbsp;&nbsp; reapply last (or referenced) stash to working dir and remove stash  
&nbsp;&nbsp;&nbsp;&nbsp; `apply (stash)` &nbsp;&nbsp;&nbsp;&nbsp; reapply last (or referenced) stash to working dir and keep stash  
&nbsp;&nbsp;&nbsp;&nbsp; `branch <branch> (stash)` &nbsp;&nbsp;&nbsp;&nbsp; create branch from stashed branch and pop stash  

`git commit`  
&nbsp;&nbsp;&nbsp;&nbsp; `--no-verify` &nbsp;&nbsp;&nbsp;&nbsp; skip git hooks  
&nbsp;&nbsp;&nbsp;&nbsp; `--amend` &nbsp;&nbsp;&nbsp;&nbsp; add staged changes to last commit. Rewrite last commit message  
&nbsp;&nbsp;&nbsp;&nbsp; `--no-edit` &nbsp;&nbsp;&nbsp;&nbsp; amend without rewriting last commit message  

`git revert ref` &nbsp;&nbsp;&nbsp;&nbsp; creates new commit, that reverts changes from rev  
`git revert oldRef^..newRef` &nbsp;&nbsp;&nbsp;&nbsp; reverts all changes from `oldRef` excluded (^ included) to `newRef`. Each revert is own commit  
&nbsp;&nbsp;&nbsp;&nbsp; `-n` &nbsp;&nbsp;&nbsp;&nbsp; does not commit the revert. Changes will be staged  

`git bisect start badRef goodRef` &nbsp;&nbsp;&nbsp;&nbsp; init bisect session. Determine first the new bad `ref` then the last known good one  
`git bisect run <script>` &nbsp;&nbsp;&nbsp;&nbsp; run the script to verify the state of codebase. I.E. `npm test`. Git will use binary search to find the first commit that breaks the `<script>`  
`git bisect good | bad` &nbsp;&nbsp;&nbsp;&nbsp; manual determination of good or bad state  
`git bisect reset` &nbsp;&nbsp;&nbsp;&nbsp; move `HEAD` to original position  

`git tag` &nbsp;&nbsp;&nbsp;&nbsp; show all tags  
`git tag 1.5.8 ref` &nbsp;&nbsp;&nbsp;&nbsp; create tag  
&nbsp;&nbsp;&nbsp;&nbsp; `-a` &nbsp;&nbsp;&nbsp;&nbsp; message  
&nbsp;&nbsp;&nbsp;&nbsp; `-s` &nbsp;&nbsp;&nbsp;&nbsp; signed  
&nbsp;&nbsp;&nbsp;&nbsp; `-f` &nbsp;&nbsp;&nbsp;&nbsp; move existing tag to another `ref`  

### Branches

`git checkout <branch>` &nbsp;&nbsp;&nbsp;&nbsp; checkout branch, creates local tracking branch if `<branch>` is a remote branch  
&nbsp;&nbsp;&nbsp;&nbsp; `-b featureX (ref)` &nbsp;&nbsp;&nbsp;&nbsp; create and checkout a new branch (from `ref`)  
`git checkout ref` &nbsp;&nbsp;&nbsp;&nbsp; move `HEAD` without connecting it to a branch  
`git checkout -` &nbsp;&nbsp;&nbsp;&nbsp; switch to last branch  

`git branch` &nbsp;&nbsp;&nbsp;&nbsp; show local branches  
&nbsp;&nbsp;&nbsp;&nbsp; `-a` &nbsp;&nbsp;&nbsp;&nbsp; show local and remote branches  
&nbsp;&nbsp;&nbsp;&nbsp; `-v` &nbsp;&nbsp;&nbsp;&nbsp; show also last commit for each branch  
&nbsp;&nbsp;&nbsp;&nbsp; `-vv` &nbsp;&nbsp;&nbsp;&nbsp; show remote tracking branches  
&nbsp;&nbsp;&nbsp;&nbsp; `-r` &nbsp;&nbsp;&nbsp;&nbsp; show remote branches  
&nbsp;&nbsp;&nbsp;&nbsp; `-f <branch> ref` &nbsp;&nbsp;&nbsp;&nbsp; move branch label to `ref`  
&nbsp;&nbsp;&nbsp;&nbsp; `--merged` &nbsp;&nbsp;&nbsp;&nbsp; show branches that are merged into `HEAD`  
&nbsp;&nbsp;&nbsp;&nbsp; `--no-merged` &nbsp;&nbsp;&nbsp;&nbsp; show branches that are NOT merged into `HEAD`  
&nbsp;&nbsp;&nbsp;&nbsp; `--contains ref` &nbsp;&nbsp;&nbsp;&nbsp; show branches with that commit  
`git branch <name> (ref)` &nbsp;&nbsp;&nbsp;&nbsp; create branch (from `ref`)  
&nbsp;&nbsp;&nbsp;&nbsp; `-m old new` &nbsp;&nbsp;&nbsp;&nbsp; rename branch from old to new  
&nbsp;&nbsp;&nbsp;&nbsp; `-d <name>` &nbsp;&nbsp;&nbsp;&nbsp; delete branch  

`git merge ref` &nbsp;&nbsp;&nbsp;&nbsp; replay all unique commits in `refs` history to `HEAD`, create 1 commit from the changes with two parents: `HEAD` & `ref`, move `HEAD` to new commit  
&nbsp;&nbsp;&nbsp;&nbsp; `--squash` &nbsp;&nbsp;&nbsp;&nbsp; replay all commits but do not commit (changes are staged). The commit will be one normal commit with one parent (no merge commit)  
`git merge-base ref1 ref2` &nbsp;&nbsp;&nbsp;&nbsp; show hash of first common ancestor  

#### Merge Conflicts

`git log --oneline --left-right --merge -p` &nbsp;&nbsp;&nbsp;&nbsp; show logs and diffs that contributed to conflict  
`git diff` &nbsp;&nbsp;&nbsp;&nbsp; show merge conflicts  
`git mergetool` &nbsp;&nbsp;&nbsp;&nbsp; vimdiff `:diffget RE` (remote), `BA` (base), `LO` (local). ]c next [c  previous conflict  

#### Advanved Merges
https://git-scm.com/book/en/v2/Git-Tools-Advanced-Merging  

`git cherry-pick ref` &nbsp;&nbsp;&nbsp;&nbsp; replays commit to current branch  
`git cherry-pick oldRef^..newRef` &nbsp;&nbsp;&nbsp;&nbsp; replays commits to current branch. `oldRef` is excluded (^ included)  

`git rebase ref` &nbsp;&nbsp;&nbsp;&nbsp; rebase current branch to `ref`. Same as `git rebase ref HEAD`  
&nbsp;&nbsp;&nbsp;&nbsp; `--exec <script>` &nbsp;&nbsp;&nbsp;&nbsp; replay 1 commit at a time and test if script passes (ie 'npm test'). Stop when fails  
`git rebase ref1 ref2` &nbsp;&nbsp;&nbsp;&nbsp; rebase `ref2` to `ref1`  
`git rebase --onto ref ref1^ (ref2)` &nbsp;&nbsp;&nbsp;&nbsp; rebase selected commits on `ref` from `ref1` excluded (^ included) until `HEAD` (until `ref2`)  
`git rebase -i ref^` &nbsp;&nbsp;&nbsp;&nbsp; squash multiple commits. From `ref` excluded (^ included) to `HEAD`  
&nbsp;&nbsp;&nbsp;&nbsp; `edit` &nbsp;&nbsp;&nbsp;&nbsp; use to split commits. Type git reset `HEAD`^ to put changes in workdir. Commit manually  

`git filter-branch` &nbsp;&nbsp;&nbsp;&nbsp; rewrite complete branch. i.e. remove file from history, change email of commiter etc. See man-page  

## Config

`git config --global` (~/.gitconfig) | `--local` (.git/config) | `--system` (/etc/gitconfig)  
`git config [--global] --list`  
`git config --global user.name ""`  
  
## Remote Work

`git remote -v` &nbsp;&nbsp;&nbsp;&nbsp; show configuration for remote repos  
`git remote add origin git@github.com:account/repository.git` &nbsp;&nbsp;&nbsp;&nbsp; add remote repo  
`git remote rm origin` &nbsp;&nbsp;&nbsp;&nbsp; remove origin from config (origin is the exchanable name)  
`git remote show origin` &nbsp;&nbsp;&nbsp;&nbsp; get info for all branches at origin (calls the origin server), their handling locally and sync state  

`git push` &nbsp;&nbsp;&nbsp;&nbsp; push to remote repo  
&nbsp;&nbsp;&nbsp;&nbsp; `origin branch(:remoteBranch)` &nbsp;&nbsp;&nbsp;&nbsp; leave (:remoteBranch) out if its the same name  
&nbsp;&nbsp;&nbsp;&nbsp; `-u origin branch[:remoteBranch]` &nbsp;&nbsp;&nbsp;&nbsp; first push (-u sets upstream info to origin/branch)  
&nbsp;&nbsp;&nbsp;&nbsp; `origin :branch` &nbsp;&nbsp;&nbsp;&nbsp; delete remote branch  
&nbsp;&nbsp;&nbsp;&nbsp; `origin --delete branch` &nbsp;&nbsp;&nbsp;&nbsp; delete remote branch  
&nbsp;&nbsp;&nbsp;&nbsp; `--tags` &nbsp;&nbsp;&nbsp;&nbsp; push tags  
&nbsp;&nbsp;&nbsp;&nbsp; `<tag>` &nbsp;&nbsp;&nbsp;&nbsp; push one tag  
&nbsp;&nbsp;&nbsp;&nbsp; `-f` &nbsp;&nbsp;&nbsp;&nbsp; force push. Rewrite history  

`git branch -u origin/branch (branch)` &nbsp;&nbsp;&nbsp;&nbsp; sets upstream info to origin/branch (use current branch if missing)  
`git fetch [origin]`  get remote changes  
&nbsp;&nbsp;&nbsp;&nbsp; `--all` &nbsp;&nbsp;&nbsp;&nbsp; fetch all remotes  
`git merge origin/branch`  merge remote changes into local branch  
`git pull` &nbsp;&nbsp;&nbsp;&nbsp; fetch and merge. If upstream is set  
&nbsp;&nbsp;&nbsp;&nbsp; `--rebase` &nbsp;&nbsp;&nbsp;&nbsp; rebase local work onto remote branch instead of merging  
`git pull origin branch` &nbsp;&nbsp;&nbsp;&nbsp; fetch and merge. If no upstream is set  

### 3 Way Workflow

#### Initial setup:
`git remote add upstream <ssh url of original repo>`  
`git fetch upstream`  

`git branch --set-upstream-to upstream/master master`  

#### Create branch & set upstream to origin/branch
`git checkout -b pr/mypullrequest`  
(make changes)  
`git push -u origin pr/mypullrequest`  

#### Rebase commits
(in pr/mypullrequest branch)  
`git fetch upstream`  
`git rebase -i upstream/master` &nbsp;&nbsp;&nbsp;&nbsp; replay own commits to upstream master  
`git push -f`  

## Git Plumbing

`git cat-file -p ref` &nbsp;&nbsp;&nbsp;&nbsp; show contents of git objects (commit, tree, blob)  
&nbsp;&nbsp;&nbsp;&nbsp; `-t` &nbsp;&nbsp;&nbsp;&nbsp; show type of object (commit, tree, blob)  
&nbsp;&nbsp;&nbsp;&nbsp; `<commitRef>^{tree}` &nbsp;&nbsp;&nbsp;&nbsp; show the tree contents in the commit, not the commit itself  
`git rev-parse ref` &nbsp;&nbsp;&nbsp;&nbsp; show SHA-1 of `ref`  
`git ls-tree -r ref` &nbsp;&nbsp;&nbsp;&nbsp; f show contents of tree object (`-r` recursively)  
`git gc` &nbsp;&nbsp;&nbsp;&nbsp; run garbage collection and remove all unreferenced objects  
