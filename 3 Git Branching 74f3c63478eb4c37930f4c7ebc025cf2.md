# 3. Git Branching

### Date: May 1, 2024

### Topic: Branches in a Nutshell

### Recall

What exactly is a git commit?

Latest commits point to previous commits.

What exactly is  a git branch?

What is the HEAD pointer?

### Notes

- Git commit saves a commit object that points to the current state of your repo aka snapshot.

![Commit and Tree](3%20Git%20Branching%2074f3c63478eb4c37930f4c7ebc025cf2/Untitled.png)

Commit and Tree

- The next commit will have a pointer to this commit.

![Untitled](3%20Git%20Branching%2074f3c63478eb4c37930f4c7ebc025cf2/Untitled%201.png)

- Git branch is a lightweight movable pointer to one of the commits.
- When we create a new branch it creates a pointer to the same commit we are currently working on.
- The current branch that is being worked on is pointed to by HEAD pointer, `git log --decorate` can be used to check this.

<aside>
📌 **SUMMARY: git commit is a pointer to a snapshot of the directory and git branch is a pointer to one of the commit.**

</aside>

---

### Date: May 1, 2024

### Topic: Switching Branches

### Recall

How to move the HEAD pointer?

Branch commits always create a new commit pointing back to the initial commit.

### Notes

- `git checkout <branch>` will move the HEAD pointer to that branch.
- If we make a new commit to that branch the commit will point back to the commit which is pointed to by the master branch.

![Untitled](3%20Git%20Branching%2074f3c63478eb4c37930f4c7ebc025cf2/Untitled%202.png)

- Now, if we switch back to master and create commits, we will create a divergent history.

![Untitled](3%20Git%20Branching%2074f3c63478eb4c37930f4c7ebc025cf2/Untitled%203.png)

- This also makes merging branches easily because their parent is known.

<aside>
📌 **SUMMARY: Git branches can be switched using git checkout and can create a tree based structure of commits when working on a project.**

</aside>

---

### Date: May 7, 2024

### Topic: Basic Merging

### Recall

Keep in mind with which branch the changes will get merged with.

Merge conflicts occurs only on editing same part of the code on the same file.

### Notes

- Merge creates a new snapshot using the most recent ancestor of the two branches.
- Checkout the branch you want to merge with and write `git merge branch_name` .

`$ git checkout master
  Switched to branch 'master'
  $ git merge iss53
  Merge made by the 'recursive' strategy.`

- Merge conflicts occurs when same part of the same file has been modified on two different branches. Something like:

`<<<<<<< HEAD:index.html
  <div id="footer">contact : email.support@github.com</div>
  =======
  <div id="footer">`
   `please contact us at support@github.com
  </div>
  >>>>>>> iss53:index.html`

- Here master and iss53 branches have different content in index.html.
- We need to choose between either code above or below ========.
- After resolution we need to add the files again to mark the conflict as resolved
- `git branch --merged` gives a list of branch merged and using `--no-merged` option gives those that are not merged into the current branch that is checked out.

<aside>
📌 **SUMMARY: Switch to the branch you would like to merge changes to and in case of merge conflicts, you can either accept/reject either one of the code on the branches.**

</aside>

---

### Date: May 7, 2024

### Topic: Branch Name

### Recall

Consultation required to rename master branch, it may break everything.

### Notes

- `git branch --move old_branch_name new_branch_name` can be used to rename branches.
- To reflect this on the remote, use `git push --set-upstream origin new_branch_name` .
- To delete old branch use `git push origin --delete old_branch_name.`

<aside>
📌 **SUMMARY: `--move` argument can help rename branches locally, these renamed branches can be pushed to remote and the old branches on remote will need deletion.**

</aside>

---

### Date: May 7, 2024

### Topic: Branching Workflows

### Recall

Remote branches are always named as remote_name/branch.

### Notes

- Branches that are short lived and used for a single particular feature are called topic branches.
- Remote branches are named as remote/branch like `origin/master.`
- To get changes from remote branches we use `git fetch.` This updates our origin/branch contents.

<aside>
📌 **SUMMARY: Use `git fetch` to pull remote branch contents to your local.**

</aside>

---

### Date: May 8, 2024

### Topic: Tracking Branches

### Recall

Upstream tells which local branch is corresponding to the remote branch.

### Notes

- Local branches that have a direct connection with remote branch.
- When we track local branch with remote branch, `git pull` will bring all the latest remote changes to your local branch.
- Use `git checkout --track origin/serverfix` to create a local serverfix branch that tracks the remote one.
- To see the branches that are being tracked and their ahead/behind status:

`git branch -vv
    iss53     7e424c3 [origin/iss53: ahead 2] Add forgotten brackets
    master    1ae2a45 [origin/master] Deploy index fix`

<aside>
📌 **SUMMARY: Tracked branches are branches that have a corresponding remote branch.**

</aside>

---

### Date: May 8, 2024

### Topic: Rebasing

### Recall

Rebasing is no different than merge.

Rebasing helps give clean history.

Mostly used when contributing.

### Notes

- Rebasing is another way of merging branches.
- In rebasing the branch to be merged is updated with patches made i.e. the diff statements.
- `git checkout experiment & git rebase master` results in following:
    
    ![Screenshot 2024-05-08 at 15.51.35.png](3%20Git%20Branching%2074f3c63478eb4c37930f4c7ebc025cf2/Screenshot_2024-05-08_at_15.51.35.png)
    
- `git checkout master & git merge experiment` results in a fast-forward merge:

![Screenshot 2024-05-08 at 15.55.42.png](3%20Git%20Branching%2074f3c63478eb4c37930f4c7ebc025cf2/Screenshot_2024-05-08_at_15.55.42.png)

- End product of rebase is no different than merge.
- The only difference is in the merge log history, which appears as a series.
- Rebase is used when contributing to a repo, so that the merger only needs to do fast forward merge and the merge is cleaner.

<aside>
📌 **SUMMARY: Rebase is another way to do merge in fast forward way and keeping a clean log.**

</aside>

---

[4. Git Internals](https://www.notion.so/4-Git-Internals-930402b37f71418fb2852aaa6efb06b7?pvs=21)