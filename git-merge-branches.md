- Login to storage server and switch to root user for ease of task
- Change directory to /usr/src/kodekloudrepos/demo and list the current files/directories

```
# cd /usr/src/kodekloudrepos/demo
# ls -ltr
```

- Check the current branches present on the git repo
```
# git branch -a
```

- Create new branch by executing the command
```
# git checkout -b xfusion
```

- Copy the file index.html to your repo
```
# cp /tmp/index.html .
```

- Add and commit the changes in your repo
```
# git add .
# git commit -m 'added index.html'
```

- Switch to master branch where the changes have to be merged
```
# git checkout master
```

- Execute git merge to merge the changes from the new branch into master
```
# git merge xfusion
```

- Push to the changes to origin repository
```
# git push origin master
```