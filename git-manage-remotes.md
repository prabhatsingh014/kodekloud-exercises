- Go to the cloned directory and check the git repository content, current branch and current remotes configured
```
$ cd /usr/src/kodekloudrepos/games/
$ ls -ltr
$ sudo git status
$ sudo git branch
$ sudo git remote -v
```

- Add new remote as per the details given in the question
```
$ sudo git remote add dev_games /opt/xfusioncorp_games.git
```

- Verify if the git remote has been added correctly with the name
```
$ git remote -v
```

- Copy the file from tmp directory to the current directory
```
$ sudo cp /tmp/index.html .
```

- Check the untracked files in the git cloned repository
```
$ sudo git status
```

- Add the untracked file to the staging
```
$ sudo git add .
```

- Commit your changes locally in the current branch
```
$ sudo git commit -m 'added index.html'
```

- Push your changes to the remote repository (created earlier)
```
$ sudo git push dev_games master
```