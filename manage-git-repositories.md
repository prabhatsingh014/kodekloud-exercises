thor@jump_host ~$ ssh max@ststor01
The authenticity of host 'ststor01 (172.16.238.15)' can't be established.
ECDSA key fingerprint is SHA256:0z85j/k+4Nf8WKbHJzxo1AOv4FeRA8LPET2N3BEkYyo.
ECDSA key fingerprint is MD5:74:e6:4d:c4:b3:80:07:be:03:30:0a:bf:1e:eb:e6:82.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'ststor01,172.16.238.15' (ECDSA) to the list of known hosts.
max@ststor01's password: 
Welcome to xFusionCorp Storage server.
max $ 
max $ cpwd
-bash: cpwd: command not found
max $ pwd
/home/max
max $ git clone ^C
max $ git clone http://git.stratos.xfusioncorp.com/max/story_media.git
Cloning into 'story_media'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
max $ ls -ltr
total 4
drwxr-sr-x    3 max      max           4096 Mar 11 11:01 story_media
max $ 
max $ ls -l /usr/devops/
total 8
-rw-r--r--    1 max      max            792 Mar 11 10:56 frogs-and-ox.txt
-rw-r--r--    1 max      max           1086 Mar 11 10:56 lion-and-mouse.txt
max $ cp -rp /usr/devops/* story_media/
max $ ls -ltr story_media/
total 8
-rw-r--r--    1 max      max           1086 Mar 11 10:56 lion-and-mouse.txt
-rw-r--r--    1 max      max            792 Mar 11 10:56 frogs-and-ox.txt
max $ cd story_media/
max $ git branch
max $ git add .
max $ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   frogs-and-ox.txt
        new file:   lion-and-mouse.txt

max $ git commit -m "add stories"
[master (root-commit) f8ba066] add stories
 Committer: Linux User <max@ststor01.stratos.xfusioncorp.com>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 2 files changed, 42 insertions(+)
 create mode 100644 frogs-and-ox.txt
 create mode 100644 lion-and-mouse.txt
max (master)$ git push -u origin master
Username for 'http://git.stratos.xfusioncorp.com': max
Password for 'http://max@git.stratos.xfusioncorp.com': 
Counting objects: 4, done.
Delta compression using up to 36 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 1.19 KiB | 0 bytes/s, done.
Total 4 (delta 0), reused 0 (delta 0)
remote: . Processing 1 references
remote: Processed 1 references in total
To http://git.stratos.xfusioncorp.com/max/story_media.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
max (master)$ git checkout -b max_demo
Switched to a new branch 'max_demo'
max (max_demo)$ cp /tmp/stories/story-index-max.txt .
max (max_demo)$ vi story-index-max.txt 
max (max_demo)$ git status
On branch max_demo
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        story-index-max.txt

nothing added to commit but untracked files present (use "git add" to track)
max (max_demo)$ git add .
max (max_demo)$ git commit -m "typo fixed for Mooose"
[max_demo b8e6369] typo fixed for Mooose
 Committer: Linux User <max@ststor01.stratos.xfusioncorp.com>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 4 insertions(+)
 create mode 100644 story-index-max.txt
max (max_demo)$ git push -u origin max_demo
Username for 'http://git.stratos.xfusioncorp.com': max
Password for 'http://max@git.stratos.xfusioncorp.com': 
Counting objects: 3, done.
Delta compression using up to 36 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 413 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: 
remote: Create a new pull request for 'max_demo':
remote:   http://git.stratos.xfusioncorp.com/max/story_media/compare/master...max_demo
remote: 
remote: . Processing 1 references
remote: Processed 1 references in total
To http://git.stratos.xfusioncorp.com/max/story_media.git
 * [new branch]      max_demo -> max_demo
Branch max_demo set up to track remote branch max_demo from origin.
max (max_demo)$ 
max (max_demo)$ 