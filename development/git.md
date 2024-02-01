# Git Stuff

- [Git Stuff](#git-stuff)
  - [Working on a branch notes](#working-on-a-branch-notes)
  - [Git Submodules](#git-submodules)
  - [Git tools](#git-tools)
  - [Git tips](#git-tips)
    - [Git Bash in Windows](#git-bash-in-windows)
    - [Credentials management Configuration](#credentials-management-configuration)
    - [SSH keys with git commands](#ssh-keys-with-git-commands)
      - [Git pull using an ssh key](#git-pull-using-an-ssh-key)
    - [Long file paths workaround](#long-file-paths-workaround)
    - [Reset to version in HEAD](#reset-to-version-in-head)
    - [Get rid of local changes to a file before they are added](#get-rid-of-local-changes-to-a-file-before-they-are-added)
    - [Reflog - getting out of trouble](#reflog---getting-out-of-trouble)
    - [Check where your remote repo is - e.g. personal, main repo, fork etc](#check-where-your-remote-repo-is---eg-personal-main-repo-fork-etc)
    - [Comparing with previous version (works for file or dir) - useful after pull](#comparing-with-previous-version-works-for-file-or-dir---useful-after-pull)
    - [Seeing a large diff in the command line to compare a remote to your repo](#seeing-a-large-diff-in-the-command-line-to-compare-a-remote-to-your-repo)
    - [Checking out the latest version based on tag](#checking-out-the-latest-version-based-on-tag)
    - [Pulling in a remote Pull Request to a local repo](#pulling-in-a-remote-pull-request-to-a-local-repo)
    - [Why don't I see all remote branches? Getting all branches when there are multiple remotes defined](#why-dont-i-see-all-remote-branches-getting-all-branches-when-there-are-multiple-remotes-defined)
    - [Using a Pull Request version in dependencies pom.xml](#using-a-pull-request-version-in-dependencies-pomxml)
    - [Amending a git commit even if already pushed](#amending-a-git-commit-even-if-already-pushed)
    - [Example from bitbucket docs on resolving merge conflict (TODO - merge with Merges section far below in the training notes)](#example-from-bitbucket-docs-on-resolving-merge-conflict-todo---merge-with-merges-section-far-below-in-the-training-notes)
    - [Git Rebasing](#git-rebasing)
    - [**Links**](#links)
    - [.gitignore](#gitignore)
    - [Keeping in synch with upstream repo](#keeping-in-synch-with-upstream-repo)
    - [Copying a repo including branches and history](#copying-a-repo-including-branches-and-history)
    - [Stashing](#stashing)
    - [Showing details of commits and trees](#showing-details-of-commits-and-trees)
    - [Adding, Committing, status and removing](#adding-committing-status-and-removing)
    - [Moving code from one repo to another keeping history](#moving-code-from-one-repo-to-another-keeping-history)
  - [Git Configuration](#git-configuration)
    - [Color on git prompt in ubuntu](#color-on-git-prompt-in-ubuntu)
  - [Notes from git basic training](#notes-from-git-basic-training)
    - [Basic git repo overview](#basic-git-repo-overview)
    - [Repository](#repository)
    - [Object Store](#object-store)
    - [Object Types](#object-types)
    - [Data Model](#data-model)
    - [Working Directory](#working-directory)
    - [Staging area](#staging-area)
    - [Files tracking](#files-tracking)
    - [Commits](#commits)
    - [Absolute Commit names](#absolute-commit-names)
      - [**Symbolic Refs**](#symbolic-refs)
    - [Relative Commit names](#relative-commit-names)
    - [Branches](#branches)
    - [Newer way of working with branches - switch and restores](#newer-way-of-working-with-branches---switch-and-restores)
    - [Merges](#merges)
    - [Example of a basic Merge](#example-of-a-basic-merge)
    - [Discarding Merges](#discarding-merges)
      - [Undo merge committed in local not yet pushed](#undo-merge-committed-in-local-not-yet-pushed)
    - [Aborting a Merge](#aborting-a-merge)
    - [Merge Types](#merge-types)
    - [Resetting a branch to a remote branch](#resetting-a-branch-to-a-remote-branch)
  - [Git workflows](#git-workflows)
  - [Differences](#differences)
    - [Difference sources](#difference-sources)
      - [**Examples**](#examples)
  - [Finding a commit](#finding-a-commit)
  - [Checking out files](#checking-out-files)
    - [Amending a commit](#amending-a-commit)
  - [Undoing a commit - git reset](#undoing-a-commit---git-reset)
    - [**Clarification of terms**](#clarification-of-terms)
  - [Rebase vs Merge + good practices](#rebase-vs-merge--good-practices)
    - [Cherry picking](#cherry-picking)
  - [Cloning, Remotes and Tracking branches](#cloning-remotes-and-tracking-branches)
  - [Tracking Branches](#tracking-branches)
    - [Working with Remotes](#working-with-remotes)
    - [Adding and deleting branches](#adding-and-deleting-branches)
    - [Configuration Stuff](#configuration-stuff)

1. Github - <https://github.com/>
2. <http://progit.org/book/ch2-0.html> book on git
3. Bitbucket - <https://bitbucket.org/dashboard/overview>

## Working on a branch notes

- Create the branch through bit bucket site.
- Locally clone the repo - can give it a different name and it will
    create the dir (ie no need to create dir specially) with master
    branch
- git fetch <branchName> && checkout (maybe not exact syntax) is the
    command to get the other branch and switch to working on it.
- Now you can work away as normal.

## Git Submodules

- A way to include a repository within another repository.
- <https://codingkilledthecat.wordpress.com/2012/04/28/why-your-company-shouldnt-use-git-submodules/>

## Git tools

- gitk -> nice visual viewer for history (like a git log but graphic + has diffs), waaaaayyyy better than looking on bitbucket
  - <https://www.atlassian.com/git/tutorials/gitk>
- tig - command line git browser (e.g. tig blame <path>) - <https://jonas.github.io/tig/doc/tig.1.html>
- git mergetool (with config for p4merge) for graphical merge
- git gui - looking at commits (install via sudo apt .... git-gui since not bundled with git, after that git gui launches it)

## Git tips

- Visualizing git history
  - Lots of nice tools here - <https://livablesoftware.com/tools-to-visualize-the-history-of-a-git-repository/>
    - Including my favourite - GOURCE :)
  - <https://www.producthunt.com/posts/github-visualizer>

### Git Bash in Windows

Also very useful Git shell window in windows can run .sh bash scripts,
so no need to have windows bat files\.....

### Credentials management Configuration

Link windows account credentials to your git-stash *This command can be
used also to refresh your credentials - just run it again and you will
be prompted for the new credentials.

```bash
git config --global credential.helper wincred
```

- Also on Win10 you might have issues with the windows credential
    manager when changing passwords -
    <https://cmatskas.com/how-to-update-your-git-credentials-on-windows/>

### SSH keys with git commands

#### Git pull using an ssh key

```bash
git -c core.sshCommand="ssh -i ~/.ssh/id_rsa_blah" clone ssh://git@github.com/~me/my-repo.git myrepo-nightly
```

### Long file paths workaround

In windows there are filepath limits which can be annoying and blocking

```bash
# Workaround in git....
git config --global core.longpaths true
```

### Reset to version in HEAD

useful when you accidentally add something you don't want to commit.

```bash
# Restoring old way
git reset -- <file>

# Newer way 
git restore .
git restore '*.c'


# Also to checkout back to the most recent HEAD
git checkout -- .
```

- Interesting article comparing them - <https://stackoverflow.com/questions/3639342/whats-the-difference-between-git-reset-and-git-checkout>

### Get rid of local changes to a file before they are added

can also get specific versions etc.

```bash
git checkout -- file
```

### Reflog - getting out of trouble

- <https://git-scm.com/docs/git-reflog>

### Check where your remote repo is - e.g. personal, main repo, fork etc

```bash
git remote -v
```

### Comparing with previous version (works for file or dir) - useful after pull

```bash
git diff feature/official-codegen@{1} feature/official-codegen MySwaggerSpec.yaml
```

### Seeing a large diff in the command line to compare a remote to your repo

```bash
# Here we compare the origin/develop branch of your repo to a different remote repo branch
git diff --word-diff-regex=. origin/develop...someOtherRepoRemote/newBranchWithChanges
```

### Checking out the latest version based on tag

```bash
git checkout $(git tag | sort | tail -1)
```

also if you're not sure about the content of a particular tag and have
access to github, bitbucket etc. you can see directly the content of the
tag to check if your expected changes are included. Can be useful when
not obvious what was on a branch when a release tag was created.

### Pulling in a remote Pull Request to a local repo

This is a newer way of doing it - see the older way below

```bash
  git fetch origin refs/pull-requests/$PR_NO/from:$LOCAL_BRANCH
```

This is useful if you'd like to get the contents of a remote pull
request in a local repo or local fork repo

There are 2 scenarios -

- You want to pull directly from the repo

```bash
    git pull origin +refs/pull-requests/2/merge
```

- Your local repo is a fork of a main repo, and the pull request is
    made to the main repo.

```bash
    git remote add upstream <upstream url>
    # To not commit the full merge do this
     git pull --no-commit --no-ff --no-tags --progress upstream +refs/pull-requests/2/merge
    # If you don't care do this
     git pull upstream +refs/pull-requests/2/merge
```

(This example is a bit more complicated since it doesn't actually merge
the changes into local

### Why don't I see all remote branches? Getting all branches when there are multiple remotes defined

If you have multiple remotes defined, the usual git fetch will not allow
you to see all remote branches locally

Instead you should fetch from the remote and then checkout onto a new
branch and give the remote branch as the branch to track

```bash
# With just one remote defined (git remote -v to check)
git fetch
git checkout feature/test

# With more than one remote defined you need create a branch and then give the remote branch as it's tracking point - e.g. in this case "origin"
git fetch
git checkout -b feature/test origin/feature/test
```

### Using a Pull Request version in dependencies pom.xml

from pom.xml:

```bash
    <digital-api-spec.version>pull-requests-672-1.1.3</digital-api-spec.version>
```

### Amending a git commit even if already pushed

```bash
    $ git commit --amend
    # CAUTION - only use the git push -f to your OWN fork of a repo and where you're sure nobody else is pushing changes (e.g. updating an open PR by amending a commit).
    $ git push -f
```

### Example from bitbucket docs on resolving merge conflict (TODO - merge with Merges section far below in the training notes)

Issues Merging the Pull Request Merge conflict This pull request has
conflicts. You must resolve the conflicts before you can merge:

- **Step 1:** Fetch the changes (saving the target branch as FETCH_HEAD).

```bash
    git fetch origin master
```

- **Step 2:** Checkout the source branch and merge in the changes from the target branch. Resolve conflicts.

```bash
    git checkout bugfix/OREPT-19-css-general-changes
    git merge FETCH_HEAD
```

- **Step 3:** After the merge conflicts are resolved, stage the changes accordingly, commit the changes and push.

```bash
    git commit
    git push origin HEAD
```

- **Step 4:** Merge the updated pull request.

### Git Rebasing

Alternative to merging - Refresh your branch with changes from another
branch → refresh feature branch from master/develop

What's the difference with a simple git merge?

- **Merge** - will introduce another commit into the history for the merge of the two branches
- **Rebase** - keeps it cleaner but REWRITES the history of the feature branch

i.e. it moves the base of the feature branch to the most recent commit
(TBC - my understanding here) and then creates new versions of the
feature branch commits after that.

```bash
 $ git checkout my-feature-branch
 $ git rebase master <my-feature-branch>
  ... resolve conflicts and then ...
 $ git rebase --continue

 # NB - you will probably have to git push -f to force the update of your remote branch after the rebase.
 # DO NOT DO THIS ON SHARED BRANCHES - or you may overwrite other people's work. It should only be on your own feature branches.
```

### **Links**

- <https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase>
- <https://nathanleclaire.com/blog/2014/09/14/dont-be-scared-of-git-rebase/>
- <https://git-scm.com/book/en/v2/Git-Branching-Rebasing>
- <https://git-scm.com/book/en/v2/Git-Branching-Rebasing>

### .gitignore

- Git ignore cheatsheet -
    <https://labs.consol.de/development/git/2017/02/22/gitignore.html>

### Keeping in synch with upstream repo

When you have forked a repo, you'll want to keep your fork in sync with
the original or "upstream" repository

```bash
# First time setup - add the upstream repo as a remote
$ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git

# check the remotes for your forked repo to see the "upstream" remote added
$ git remote -v
> origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
> upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)
> upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push)

# Update from upstream
$ git fetch upstream
$ git checkout master # or whatever branch you want to synch
$ git merge upstream/master master
$ git push # to update remote origin

# Alternative to merge - rebase
$ git rebase upstream/master
```

- A very nice explanation of git fetching and effect on branches +
    origins -
  - <https://stackoverflow.com/questions/11892517/git-fetch-vs-git-fetch-origin-master-have-different-effects-on-tracking-branch/11896392#11896392>

### Copying a repo including branches and history

- <https://www.atlassian.com/git/tutorials/git-move-repository>

```bash
# Get everything from the source repo
git clone --mirror ssh://git@git.rnd.amadeus.net/tcn/offer-ndc-touchpoint-cna.git

# Check the branches and tags
git tag
git branch -a

# Remove the origin
git remote rm origin

# Add new origin
git remote add origin ssh://git@git.rnd.amadeus.net/dapi/offer-ndc-touchpoint-cna.git

# push everything to the new origin
git push origin --all
git push --tags
```

### Stashing

```bash
# Saving current work to a stash with a message (save and message are optional)
$ git stash save "Temp Modifs"
Saved working directory and index state On feature/Blah: Temp Modifs
HEAD is now at 60bf738 Merge branch 'develop' into feature/Blah

# List current stashes
$ git stash list
stash@{0}: On feature/Blah: Temp Modifs

# TODO reapply a stash - either most recent or based on the index
$ git stash pop
$ git stash pop stash@{1}
```

### Showing details of commits and trees

```bash
# Show details of the tree of a commit
~/Development/java/openapi2puml$ git ls-tree 542ae0f6
100644 blob ad71708ae7baa4e06a376272ebd7faf0621560dd    .gitignore
100644 blob e48cb7ad36a16169f9354376026aad7c20d7956a    .travis.yml
100644 blob 261eeb9e9f8b2b4b0d119366dda99c6fd7d35c64    LICENSE
100644 blob 1d93921d429ec77e15ad6faab28ef9d94035815a    README.md
040000 tree cd46e77d34c17b54af48cbc5769eb7146d928c00    cfg
040000 tree df05e9c6087c5f8ebf981f5b5513fc4b4f4611e0    examples
040000 tree 26dc9f0ea3a708adacb8c5cf1a6419e866c477fe    openapi2puml-core
100644 blob 8e151569156627dc7fef69630ee1568e8cbb2e9c    pom.xml

# Show the details of the commit
$ git show 542ae0f6

# Show log details with one line per commit
$ git log --oneline

# show log limited
$ git log -2 # last n commits

# Some of the options are:
-- since, --after
--until, --before
--author
--grep
-S # show commits adding or removing code matching string but it's slow

# Show graph and commits in reverse order
$ git log --oneline --graph
# Show branches and then list the commits
$ git show-branch -r (or -a)

# Can also visualize with gitk - installed on ubuntu
$ gitk (inside repo)
```

### Adding, Committing, status and removing

```bash
# Automatically stages and then commits
$ git commit -a -m "Some commit message"

# Show short status
$ git status -s

# Removing file from both repo and working dir
git rm <filename>

# moving file from staged to unstaged
$ git rm --cached
```

### Moving code from one repo to another keeping history

- <https://www.atlassian.com/git/tutorials/git-move-repository>

I probably could have used git hub importer but it kept failing and I
realised it was due to my private email settings.

## Git Configuration

### Color on git prompt in ubuntu

- Colorizing git prompt
  - <https://medium.com/ag-grid/git-on-the-command-line-improving-the-experience-5a604cb14cf6>
  - <https://github.com/DarrenC/bash-git-prompt> - this is the one I use which is easy to setup :)

## Notes from git basic training

- Git is a stream of snapshots of a mini file system instead of diffs
  - So git is not considered a true VCS
- In general git only adds things to the DB
- Even just staged data is kept for 90 days
- Deletes just make something not reachable unless you know the hash id.

### Basic git repo overview

- hidden directory **.git**
  - all revision information goes in it
  - TODO - here look at pg 22-24 for objects etc.
- terminology
  - Repository
  - Object Store
  - Object Types - blobs, commits, trees, tags
  - Git data model
  - Working directory
  - Staging area

### Repository

- A database with all information to manage revisions and history of a
    project
- 2 primary data structures
  - Object Store
  - Staging Area

### Object Store

- Contains original data files, log messages, author info, dates etc
- Can be used to build any version of a project
- Contains Object Types - blobs, commits, trees, tags
- Economize space - objects compressed into pack files - stores pieces
    of data not full files
- Git - Content Tracking System - object store is content-addressable
    storage system
- SHA1 hash value on the contents of the file gives the unique name
    for each object
  - Change to a file gives new SHA1 and thus a new version
  - usually 40 digit hex number
  - Can abbreviate to a smaller unique prefix

### Object Types

- Blobs - each version of file represented as a blob
- Tree - one level of dir info - blobs, paths, other subtrees
- Commit - see below
- Tag - arbitrary human readable name for an object usually a commit
    to serve as a reference point

### Data Model

- Git data model
  - commit -> tree -> blobs (or even other trees)
  - A commit points to a tree object that captures in one snapshot
        the state of the repo when the commit was performed
  - Usually a commit has just one parent - root is the exception

### Working Directory

- Directory where .git is found
- Contains a snapshot of the repo
- Working dir changes need to be **Added** to staging area to be saved
    into the repo

### Staging area

- Also called index
- Shows what will be added with next commit command
- Temporary dynamic file to show dir structure of whole repo. Snapshot
    at a point in time
- Can be represented by a commit + tree
- Allows separation of incremental development + committing the
    changes

### Files tracking

- Tracked - file in the repo/index. Created by "\$git add"
- Ignored - declared in the .git-ignore files of the repo
- Untracked - Any other file in the repo which is not in the other two
    types

### Commits

- Single atomic changeset to a repo
- Snapshot of the staging area put in the object store
- Links always to its predecessors - i.e. not whole copy of every
    file+dir
- Can ref a commit by explicit ref or implied ref (HEAD\^2 etc.)

### Absolute Commit names

aka - Hash identifier

- commit is globally unique for all repos
- Can shorten to unique prefix

#### **Symbolic Refs**

- **HEAD:** most recent commit on current branch
- **ORIG_HEAD:** previous version of HEAD prior to adjusting
- **MERGE_HEAD:** commit being merged into HEAD
- **FETCH_HEAD:** head of last branch fetched

### Relative Commit names

- Every commit except first one has at least one earlier commit and
    maybe from multiple previous commits
- Can select previous commits using relative names
- Usually used to gather/find commits to then perform operations on
    them
- Use:
  - ^ used to select a different parent
  - ~ used to select a preceding generation of the same parent
  - Can combine e.g. Head^2~1 - commit n-1 of parent 2
  - Commit ranges
    - start..end - accessible from end but not from start
  - Symmetric difference
    - start...end - commits exclusively accessible from start or end but not both

### Branches

Branch is the way of working on a separate line of development

- Branch name is a pointer to a particular commit - the most recent
    revision committed on it - aka Tip or Head of branch
- Many branches, only one is active
- A branch moves forward incrementally, there is no info about where
    the branch originated
- The active branch
  - often implicitly used in commands
  - determines content of working directory (updating to remove/add
        as reqd. when switching branches)
  - commit always applied to the active branch
- For naming can use hierarchy e.g. feature/CRblah
- No special characters and nothing that could screw up the
    hierarchical naming (no .. or / at the end of the name) and NO
    WHITESPACE
- Can checkout different branches even with modifications on current
    branch (with conditions)
  - Untracked files from current branch - no issues
  - Modified tracked files from current branch which aren't changed
        on new checkedout branch - no issues
  - Modified tracked files changed on both current and new checkout
        branch - error - your changes would be overwritten - can
        checkout + merge
- Can also checkout:
  - commit not at HEAD of branch
  - tracking branch
  - commit refd by a tag
- Results in a detached HEAD branch situation. Can't commit directly
    to it but can create a new branch from here to make changes

```bash
# Create a branch
git branch <nameOfBranch> [starting commit]

# Checkout a branch
git checkout <nameOfBranch>

# See last commit on a branch
git branch -v

# Checkout branch with conflicting modifications to tracked files - use checkout with merge, might have to resolve conflicts manually
git checkout -m master

# Create and checkout
git checkout -b NewBranchName [commit where to start branch]

# Deleting branch - only works if there are no commits not merged
git branch -d <BranchName>

git branch -D <BranchName> # FORCE delete
```

### Newer way of working with branches - switch and restores

- Using switch and restore <https://tanzu.vmware.com/developer/blog/git-switch-and-restore-an-improved-user-experience/>

### Merges

- Unifies two or more commit history branches within a single repo
- 2 possibilities
  - No conflict - new merge commit to represent new unified state
  - conflict - requires merge of changes marked as unmerged in the
        index - manual reconciliation

### Example of a basic Merge

```bash
# Basic merge
$ git checkout destinationBranch
$ git merge sourceBranch
$ vim conflictFile (or p4merge or equivalent)
# OR
$ git mergetool
$ git commit -a
```

### Discarding Merges

- Can discard a merge even after committing.
- Basic idea is to make the merge commit unreachable.
- Could only reach that commit locally (haven't pushed yet) and would
    need to know the hash for the commit.

#### Undo merge committed in local not yet pushed

```bash
# Undo merge, reset to previous HEAD value, make merge commit unreachable
git reset --hard ORIG_HEAD
```

### Aborting a Merge

- Aborting a merge before committing any modifications etc.
- sets commit back to the HEAD

```bash
# Abort merge, reset to current HEAD value
git merge --abort

# Older way
git reset --hard HEAD
```

### Merge Types

- Already up-to-date - everything on the branch being merged in is
    already an ancestor on the destination branch - degenerate merge -
    no new commits added after performing the merge
- Fast-forward - HEAD on destination branch can be simply moved to
    latest commit on the branch being merged in since there are no local
    changes - degenerate merge - no new commits added -
    <https://git-scm.com/docs/git-merge/2.9.0#_fast_forward_merge>
- True merge - a commit is needed specifically to merge the two (or
    more) parent branches

### Resetting a branch to a remote branch

If you have a branch which has been updated by multiple remotes and
you'd like to return to the same state as a particular remote branch
you can reset.

```bash
# From your desired branch, assuming you want to reset to the origin remote, master branch current state
git fetch origin
git reset --hard origin/master
```

## Git workflows

<https://buddy.works/blog/5-types-of-git-workflows>

- Basic
- Feature Branch
- Feature Branch with Merge Requests
- GitFlow
- Forking workflow

## Differences

- Diff is in-built to Git
- Can compare files or trees
  - trees compared by commits
- Diff output:
  - Header with:
    - original file denoted by ---
    - new file denoted by +++
    - @@ line to give line number context for both versions
  - Content with prefix:
    - "-" : line deleted
    - "+" : line added
    - blank space : no change

```bash
diff --git a/pom.xml b/pom.xml
index 9e168c4..fb377eb 100644
--- a/pom.xml
+++ b/pom.xml
@@ -134,6 +134,30 @@
```

### Difference sources

- Any tree in commit graph
- Working Directory
- Staging Area

#### **Examples**

```bash
    # diff between working directory and staging area - i.e. what'll be in next commit
    $ git diff

    # differences between working dir and a given commit (e.g. HEAD, hash of commit, branch name)
    $ git diff //commit_id//

    # differences between staged changes and a given commit
    $ git diff --cached //commit_id//

    # differences between 2 given commits
    $ git diff //commit_id_1// //commit_id_2//
```

## Finding a commit

```bash
git blame <filename>
```

## Checking out files

- Checkout a file from the index

```bash
git checkout <filename>
```

- Checkout a file from a commit

```bash
git checkout HEAD <filename>
```

### Amending a commit

```bash
# Amending a commit
git commit --amend -m "New Message for the commit"

# Changing author
git commit --amend --author="Mr Test<MrTest@localhost>"
```

## Undoing a commit - git reset

The HEAD position is changed to point to a given commit, and then depending on the type of reset there are different impacts

```bash
# Soft reset
# - working directory and staging area remain the same
git reset --soft HEAD^

# Mixed reset - the DEFAULT behaviour
# - working directory remains the same but unstages any changes
git reset HEAD^

# Hard reset
# - working directory and staging area changed back to the commit tree structure, commit undone.
git reset --hard HEAD^

# Going back a number of commits from HEAD - e.g. 2 (NB - if the commits were merges it will impact both the merge commit + commits introduced by merge)
git reset HEAD~2
```

### **Clarification of terms**

- Reset - go back to a previous situation
- Revert - make a change (i.e. new commit) that changes to previous
    values

## Rebase vs Merge + good practices

- Rebase - Clean history but no idea what happened on the branch
- Merge - 1 commit showing where a branch arrived to the master

- Never rebase a branch that has published commits since this will
    mess up anyone who used that branch.
- Should be kept for your own branch

### Cherry picking

Allows you to pick a commit from one branch and apply it to another

```bash
# Source branch has a commit hash xyz123456 that is needed on the target-branch
git checkout target-branch 
git cherry-pick xyz123456
```

## Cloning, Remotes and Tracking branches

- Git repository can be cloned to allow developers to work
    autonomously without locks and merging with other clones as
    necessary
- Bare Clone - e.g. Central Repository - don't work directly with it
- Repo Clone - copy that is used for development
- Clones
  - Copy of repository - independent, autonomous, symmetric peer of
        original
  - Contains all objects from original
  - not all information is copied from original
  - local dev branches of original (refs/heads) become remote
        tracking branches in the clone (refs/remotes)
    - remote original repo branches available in clone - branch
            name prefixed with **origin/**
  - One way relationship - original knows nothing about clone

## Tracking Branches

- Branches in local repo - considered local branches but diff
    categories
  - remote-tracking branches - associated to a remote branch to
        follow changes upstream - don't modify directly
  - local-tracking branches - paired to remote-tracking branch -
        integrates changes from remote-tracking branch and your
        modifications
  - local non tracking branches - topic or development branch
  - Create a local tracking branch by checking out the name of a
        remote-tracking branch

### Working with Remotes

```bash
# Add a remote - by default origin is the only remote
git remote add upstream <upstream url>

# Operate on a remote
git fetch/pull/push [remote name][branch name]
```

- fetch - retrieve objects and related metadata from remote
- pull - like fetch but also merges changes into currently checked-out
    branch
- push - transfer objects + metadata to remote repo

### Adding and deleting branches

```bash
# Adding a local branch
git branch <newBranchName>

# Deleting local branches
git branch -d <newBranchName>

# Deleting remote-tracking branch - only in local repo not remote git
branch -d -r origin/<newBranchName>

# adding a branch to remote repo
git branch <newBranch>
git push origin <newBranch>

# deleting that branch in REMOTE only
git push origin :<newBranchName>

# push a branch that exists only in local to a remote (i.e. create on remote) and give it a new name
git push -u origin my-local-branch:my-branch-new-name
```

### Configuration Stuff

3 levels

- Repo-specific - .git/config modified with --local
- User-specific - \~/.git/config modified with --global
- System-specific - /etc/gitconfig modified with --system
