- Create the manifest file with the name news.txt at the specified location on puppet master (jump host) using root user
```
$ vi /etc/puppetlabs/code/environments/production/manifests/apps.pp

file { '/opt/data/media.txt' :
  ensure => present,
}

node 'stapp01.stratos.xfusioncorp.com' {
}
```

- Save and exit the file

- Execute the following command to validate the manifest on puppet master (jump host) using root user
```
$ puppet parser validate apps.pp
```

- Login to app server 1 and execute the following command to apply the changes using root user
```
$ puppet agent -tv
```

- Verify the creation of file
```
$ ls -l /opt/data
```