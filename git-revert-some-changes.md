- Login to storage server and switch to root user
```
$ sudo su -
```

- Switch to the git repository directory
```
# cd /usr/src/kodekloudrepos/blog
```

- Verify the commits done so far on the git repository
```
# git log --oneline
```

- Verify the commit HEAD
```
# git reflog
```

- Revert the latest commit to reach to stage of initial commit
```
# git revert 3844a58 //3844a58 --> latest commit ID
```

- Verify the header once again after revert and check the content of the repository
```
# git log --oneline
# ls -ltr
```