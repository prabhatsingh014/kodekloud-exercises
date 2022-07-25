- Login to storage server as user natasha and switch to root user
- Install git package with yum command
```
# yum install git -y
```
- Create a directory named beta.git under /opt
```
# cd /opt/
# mkdir beta.git
```
- Initialize bare repository in the directory that was just created and copy the update hook at /tmp to the hooks
```
# cd beta.git/
# git init --bare
# cp /tmp/update hooks/
```
- Clone the repository at the location /usr/src/kodekloudrepos with the name beta
```
# cd /usr/src/kodekloudrepos/
# git clone /opt/beta.git
```
- Create a new branch with name xfusioncorp_beta
```
# cd beta/
# git checkout -b xfusioncorp_beta
```
- Copy the readme.md from /tmp directory to the present directory, add, commit and push to the origin repository i.e. /opt/beta.git
```
# cp /tmp/readme.md .
# git add .
# git config --global user.name "Prabhat Singh"
# git config --global user.email prabhatsingh014@gmail.com
# git commit -m 'added readme.md'
# git push origin xfusioncorp_beta
```
- Create master branch from the branch you created earlier
```
# git checkout -b master
# git branch
```
- Try to push the master branch to the origin repository, it should not be pushed because of the hook created earlier
```
# git push origin master
```