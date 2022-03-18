## Scenario

### Your history looks something like this:
  - Add missing env var to staging workflow
  - Fix typo in staging workflow
  - Add staging workflow
  - Refactor some_query.sql
### Desired history:
  - Add staging workflow
  - Refactor some_query.sql

<hr> </hr>

## Steps to achieve that

### 1. Look at your history
```
~% git log
commit commit_hash_no_4 (HEAD -> main, origin/main, origin/HEAD)
Add missing env var to staging workflow

commit commit_hash_no_3
Fix typo in staging workflow

commit commit_hash_no_2
Add staging workflow

commit commit_hash_no_1
Refactor some_query.sql
```

### 2. Choose the commit to rebase on top of
In this case you would like to squash 3 commits:
- commit_hash_no_4
- commit_hash_no_3
- commit_hash_no_2

So you will rebase on top of ``commit_hash_no_1``:

```
~% git rebase -i commit_hash_no_1
```
An editor will open with the following content:
```
pick commit_hash_no_2
pick commit_hash_no_3
pick commit_hash_no_4

# help displayed here
```
Note that the ordering here is the opposite of what git log shows, meaning that the latest commit is on the bottom.

### 3. Manipulate commit history
At this step you have multiple options on how manipulate the commits.<br><br>
Let's suppose you like the commit message ``Add staging workflow``
<br>and don't need ``Fix typo in staging workflow``, ``Add missing env var to staging workflow``.
<br>(press `i` if you are in vim to edit)
```
pick commit_hash_no_2
f commit_hash_no_3
f commit_hash_no_4

# help will be displayed here
```

``f`` means fixup, it does the same as squash but discards the commit message.
<br>Save and exit. (in vim: press `escape` then `:wq` and enter)

### 4. Push the changes
```
~% git push --force-with-lease
```

DO NOT use ``git push -f`` or ``git push --force``.
It will overwrite the remote branch with the local branch.


``--force-with-lease`` basically checks if someone else pushed changes to the remote branch that you don't have.

<hr> </hr>

## Links
https://stackoverflow.com/questions/5189560/squash-my-last-x-commits-together-using-git

https://stackoverflow.com/questions/52823692/git-push-force-with-lease-vs-force





