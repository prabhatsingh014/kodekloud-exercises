- Login to the server with the username max and its password

- Change to its home directory
```
$ cd /home/max
```

- List the files and directory present in the directory
```
$ ls -ltr
```

- Change to the directory which is stored on gitlab
```
$ cd story-blog/
```

- Try to push the changes in the directory to the origin on gitlab
```
(master)$ git push -u origin master
```

- Output will show the error with the code merge

- Fetch the latest commit from the git origin
```
# max (master)$ git pull
```

- Output will show the merge conflicts

- Edit the file which has merge conflicts and update as required
```
# (master)$ vi story-index.txt 
```

- Below command will show the changed files/directories to be committed to the origin
```
# (master)$ git status
```

- Start committing the changes to the origin by running following commands
```
# (master)$ git add .
# (master)$ git commit -m 'fixed merge and corrected spelling'
# (master)$ git push origin master
```