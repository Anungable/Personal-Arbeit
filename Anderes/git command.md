### Sync the forked project

```shell
# Add the remote, call it "upstream":
git remote add upstream https://github.com/whoever/whatever.git

# Fetch all the branches of that remote into remote-tracking branches
git fetch upstream

# Make sure that you're on your master branch:
git checkout master

# Rewrite your master branch so that any commits of yours that
# aren't already in upstream/master are replayed on top of that
# other branch:
git rebase upstream/master
# Or don't want to rewrite
git merge upstream/master
```

### Delete local branch

```shell
git branch -d <branch_name>
```

### Sync the mirror repo

- see the current remote url status

```shell
git remote -v
```

```shell
->
origin  https://twgit03.coretronic.com/circ_fw/flight-control/px4-autopilot.git (fetch)
origin  https://github.com/PX4/PX4-Autopilot.git (push)
```

upstream跟origin分開處理：upstream連動到github，origin為mirror repo

- set fetch and push remote 

```shell
git remote set-url --push origin https://twgit03.coretronic.com/circ_fw/flight-control/px4-autopilot.git
```

- set upstream (從這裡pull原始repo的更新)

```shell
git remote add upstream https://twgit03.coretronic.com/circ_fw/flight-control/px4-autopilot.git
```

### Push a specific comment

```shell
git push <remotename> <commit SHA>:<remotebranchname>
# or to autocreate a remote branch
git push <remotename> <commit SHA>:refs/heads/<remotebranchname>
```

### Reset a commit and push to remote

```shell
git reset --hard HEAD~1 #reset to the latest, or 2(the second latest) and likewise
git push --force origin <branch>
```

### Merge the branch with only 1 commit

```shell
git merge --squash <feature branch>
git commit -m "commit"
```

### Delete Local/Remote Commit

```shell
# discard all changes
git reset --hard <hash>
# keep the changes
git reset --soft <hash>

# delete most recent commit
git reset --hard HEAD~1
```

刪除遠端commit：

```shell
git push origin HEAD --force
```

