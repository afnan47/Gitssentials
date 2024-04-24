# 2. Git Basics

### Date: April 21, 2024

### Topic: git clone

### Recall

What is git clone?

What all protocols does git clone support?

### Notes

- Usage: `git clone <repo_name> <optional_directory_name>`
- Clones the full data that the server has, with each and every version.
- `<repo_name>` can use https or git or user@server protocol. Eg: [https://github.com/libgit2/libgit2](https://github.com/libgit2/libgit2)

<aside>
📌 **SUMMARY: `git clone` makes a full copy of the data with all its versions and checks out on the latest version.**

</aside>

---

### Date: April 21, 2024

### Topic: Checking three states of files

### Recall

How to check the staged/committed status of files

### Notes

- `git status` tells
    - the state of files: staged/committed
    - the branch we are on
    - If we have switched from same branch on the server.
- add `-s`or `--short` to git status as an argument to get concise and simplified status output.

<aside>
📌 **SUMMARY: `git status` command helps getting the status of untracked files and the current branch.**

</aside>

---

### Date: April 21, 2024

### Topic: Ignoring files

### Recall

How to protect some files from being staged or being mentioned untracked by git?

What file pattern standard does gitignore follow?

### Notes

- Create a file `.gitignore` that contains class of files you don’t want to add to git or show as untracked.

```bash
$ cat .gitignore
# File extensions ending in o or a.
*.[oa] 
# File name ending in ~
*~ 
# ignore all .a files
*.a
# but do track lib.a, even though you're ignoring .a files above
!lib.a
# only ignore the TODO file in the current directory, not subdir/TODO
/TODO
# ignore all files in any directory named build
build/
# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt
# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf
```

- Rules to create file pattern:
    - Blank lines or lines starting with # are ignored.
    - Standard glob patterns work, and will be applied recursively throughout the entire working
    tree.
    - You can start patterns with a forward slash (/) to avoid recursivity.
    - You can end patterns with a forward slash (/) to specify a directory.
    - You can negate a pattern by starting it with an exclamation point (!).

<aside>
📌 **SUMMARY: To avoid staging files or being mentioned as untracked by git we mention those files as their name or using pattern in a file `.gitignore`**

</aside>

---

### Date: April 22, 2024

### Topic: View staged and unstaged changes

### Recall

What is git diff?

git difftool can help give a visual representation of the changes made.

### Notes

- `git diff` command helps:
    - Identify files that have modified but unstaged.
    - Identify Files that have staged we are about to commit.
    - Tell the exact lines added/removed like a patch.
- `--staged` argument helps tell the difference between staged and last commit.

<aside>
📌 **SUMMARY: To get a verbose status of our modified files we can use `git diff` .**

</aside>

---

### Date: April 23, 2024

### Topic: Committing Your Changes

### Recall

What is git commit command?

Can git commit work without a message?

### Notes

- `git commit`
- Helps push changes to stage.
- The command opens a default editor(vim/emac) highlighting the changes like git status, and also shows a blank commit message which we can add before exiting the editor.
- `git commit` with empty commit message cannot be used.
- Add messages using `-m` argument.

<aside>
📌 **SUMMARY: `git commit` pushes the code to staging area, commit messages are mandatory**

</aside>

---

### Date: April 23, 2024

### Topic: Skipping the staging area

### Recall

Is it possible to commit directly without tracking the files to stage?

Which files does `-a` use in commit?

### Notes

- Say we have added all the files we need to stage using `git add` and then committed them using `git commit` .
- If its only those files we shall modify and no new files would be added, we will need to track those files again using `git add`.
- Instead we can directly use `git commit` with `-a` flag, skipping the `git add` command.
- `-a` flag will add all of the files in the commit which were tracked during our last commit.

<aside>
📌 **SUMMARY: To skip the `git add` command and use the files that were tracked in the last commit we can use `git commit -a`**

</aside>

---

### Date: April 23, 2024

### Topic: Un-track files

### Recall

What command is used to untrack files?

Files have been staged and are to be removed, what flag must be used?

### Notes

- `git rm filename`  : To remove the file from staging area.
- Add the `-f` flag if the files is already staged to force removal.
- Add `--cached` flag to remove the file from the staging area but keep on your filesystem.
- The `filename` can be specified as an glob to remove large number of files.

<aside>
📌 **SUMMARY: Use `git rm` to remove a file from being tracked and use `-f` flag to force removal from staging area.**

</aside>

---

### Date: April 23, 2024

### Topic: Moving Files

### Recall

One of the methods used to rename files?

### Notes

- To rename files or move files between git directories we can use `git mv org_file new_file`

<aside>
📌 **SUMMARY: To move files between directories or rename the files we can use `git mv`**

</aside>

---

### Date: April 23, 2024

### Topic: Viewing the Commit History

### Recall

How to get commit history?

`git log` shows commit history from latest to oldest order.

Describe various flags that can be used to filter down log outputs?

### Notes

- `git log` provides a list of commit history made and their commit message.
- Adding `-p` or `--patch` flag with `-2` determines the number of commit history you would get.
- `--stat` flag provided statistics: lines removed/added.
- `—pretty` flag prints only the SHA-1 value of the commit and the message.
    - it can take argument `=format:"%h - %an..."` and you can print only those certain details of commit you wanna see.
- `-S keyword`  Can provide a list of commits which changed a `keyword` which can be a function name.
- `git log -- path/to/file` will provide logs that included modification to that particular path.

<aside>
📌 **SUMMARY: Use `git log` to get a history of commits made, its flags and arguments provide flexible way to filter through logs.**

</aside>

---

### Date: April 23, 2024

### Topic: Undo Commits

### Recall

How to overwrite previous commits made?

### Notes

- Consider after committing files, we forget to add some more modified or screwed up the commit message.
- Use `git commit --amend` for this.
- Overwrites last commit.

<aside>
📌 **SUMMARY: We can overwrite previous commits using `--amend` and add files to be staged and edit commit message.**

</aside>

---

### Date: April 24, 2024

### Topic: Un-stage staged files

### Recall

How to remove files from being committed to?

### Notes

- Use `git reset HEAD <file>` to unstage a file i.e remove it from getting committed.

<aside>
📌 **SUMMARY: `git reset` is gives the reverse effect of git add.**

</aside>

---

### Date: April 24, 2024

### Topic: Revert back to last commit

### Recall

Will local directory changes be lost after checkout?

### Notes

- `git checkout -- <file>` helps discard your working directory changes and revert the file contents as they were on your last commit.

<aside>
📌 **SUMMARY: `git checkout -- <file>` help restore last commit contents of that file, discarding any uncommitted modifications that we made.**

</aside>

---

### Date: April 24, 2024

### Topic: Reverting using `git restore`

### Recall

Difference between usage of `git reset` `git restore` and `git checkout` 

### Notes

- Git version ≥2.23.0 added `restore` argument to revert back things and recommends using it instead of `reset`.
- Use `git restore --staged <file>` to remove file from staging.
- Use `git restore <file>` to discard changes and restore file contents from last commit.

<aside>
📌 **SUMMARY: `git restore` is the all in one solution to restore file from being committed and restoring file contents from the latest commits.**

</aside>

---

### Date: April 24, 2024

### Topic: Working with Remotes

### Recall

How to work remote servers using git?

We can name our git servers.

### Notes

- `git remote` provides a list of remote servers we have configured with default server handle being `origin` .
- `git remote add <shortname> <url>` can be used to add your current git repository as remote repository
- Shortname can be your choice of server handle name which is origin by default.

<aside>
📌 **SUMMARY: `git remote` helps add a remote destination to which a file must be uploaded to**

</aside>

---

### Date: April 24, 2024

### Topic: Fetch Remote files

### Recall

How to download changes in remote repo?

After fetching from remote can we work simultaneously with it and our local branches/data?

### Notes

- `git fetch <shortname>` can be used to fetch all the remote changes made by a server, that we can access locally. We switch to different server names using `shortname/branch_name` .
- `git fetch` only downloads the remote data and does not merge with your local git directory, that must be done manually.
- `git pull` not only fetches the remote changes but also merges it with our local files.

<aside>
📌 **SUMMARY: Server files can downloaded using `git fetch` and manually merged or can be fetched using `git pull` which does the merging for us.**

</aside>

---

### Date: April 24, 2024

### Topic:

### Recall

### Notes

- 
- 

<aside>
📌 **SUMMARY:**

</aside>

---

### Date: April 24, 2024

### Topic: Push changes to remote

### Recall

How to update local changes made to remote?

### Notes

- `git push <remote> <branch>` to push changes to a remote.
- `git push` can not be done concurrently by two or more person at the same time.

<aside>
📌 **SUMMARY: `git push` can be used to push changes from one of your local branch to a remote server**

</aside>

---

### Date: April 24, 2024

### Topic: Inspecting a remote

### Recall

How to get an overall view of the remote server?

### Notes

- `git remote show <remote>` can be used to get details about a remote server such as the default-origin.
- Output:

`$ git remote show origin
  * remote origin
    Fetch URL: https://github.com/schacon/ticgit
    Push  URL: https://github.com/schacon/ticgit
    HEAD branch: master`

    `Remote branches:
      master  tracked                             
      dev-branch tracked                        
    Local branch configured for 'git pull':
      master merges with remote master
    Local ref configured for 'git push':
      master pushes to master (up to date)`

<aside>
📌 **SUMMARY: `git remote show` can provide details about the remote server.**

</aside>

---

### Date: April 24, 2024

### Topic: Renaming and Removing Remotes

### Recall

Keywords to rename or remove a remote server?

`rm` can be used instead of `remove`

### Notes

- `git remote rename <old_name> <new_name>` can be used to rename server’s shorthand.
- `git remote remove <remote>` can be used to remove remote sever using its shorthand.

<aside>
📌 **SUMMARY: Use `rename` or `remove` arguments with git remote to do stuff implied with it.**

</aside>

---

### Date: April 24, 2024

### Topic: Tagging

### Recall

How to mark an important commit?

### Notes

- Tags help mark important points in project such as some new version releases, 2.0.0 3.1.1 etc.
- `git tag` lists out the tags created.

<aside>
📌 **SUMMARY: Specific commits can be tagged.**

</aside>

---

### Date: April 24, 2024

### Topic: Two types of tags

### Recall

Use case scenarios of the two types of tags?

### Notes

- Lightweight:
    - Pointer to a specific commit.
    - Alias to a branch that’s stagnant.
    - `git tag v1.3` can be used to create a lightweight that stores the commit checksum.
- Annotated:
    - Is a full git object.
    - They are checksummed and contain tagger name, email, date, tagging message and can be signed.
    - `git tag -a v2.0.0 -m "Bard renamed Gemini"` can created an annotated tag with `-a` flag.

<aside>
📌 **SUMMARY: Tags are of two types: shallow and detailed.**

</aside>

---

### Date: April 24, 2024

### Topic: Tagging later

### Recall

Checksum can provided as full or just a part.

### Notes

- `git tag -a <version> <checksum>` can help add tag to a particular commit using commit’s checksum.

<aside>
📌 **SUMMARY: Tags can be added to a whole history of commits**

</aside>

---

### Date: April 24, 2024

### Topic: Sharing Tags

### Recall

By default git push does not push tags.

### Notes

- To reflect tags in the remote repo use `git push origin <tagname>`
- To push all tags use `--tags` .

<aside>
📌 **SUMMARY: Tags are required to be pushed manually using git push.**

</aside>

---

### Date: April 24, 2024

### Topic: Delete tags

### Recall

Remote deletion requires push as did sharing.

### Notes

- `git tag -d <tag>` to delete a tag.
- `git push origin --delete <tagname>`	
 to delete remote tag.

<aside>
📌 **SUMMARY: To remove local tags use `-d` and`--delete` for remote tags**

</aside>

---

### Date: April 24, 2024

### Topic: Checkout Tags

### Recall

We can checkout an old tag to make some bug fixes if needed.

### Notes

- `git checkout <tag>` can help checkout old tags.

<aside>
📌 **SUMMARY: We can checkout the old state of repo using a tag.**

</aside>

---

### Date: April 24, 2024

### Topic: Git Aliases

### Recall

Can we create our own shortcuts to use git commands quickly or according to our taste?

What command is used to create aliases?

### Notes

- We can create our own aliases for any git commands such as `git push/commit/reset HEAD/log -1 HEAD`
- This can be a personal choice and may come in handy in case we use a command frequently but is quite long to be remembered or we prefer our own alias.
- Say we frequently look at our last commit then what we can do is:

`$ git config --global alias.last 'log -1 HEAD’ # last is our alias for log -1 HEAD`  

`$ git last`

  `commit 66938dae3329c7aebe598c2246a8e6af90d04646
  Author: Josh Goebel <dreamer3@example.com>
  Date:   Tue Aug 26 19:48:51 2008 +0800`

<aside>
📌 **SUMMARY: Git provides freedom to create alias for its own commands.**

</aside>

---

[3. Git Branching](3%20Git%20Branching%2074f3c63478eb4c37930f4c7ebc025cf2.md)