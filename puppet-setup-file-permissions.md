- Switch to root user on the jump host
```
$ sudo su -
```

- Change the directory to manifests and create the manifest file with media.pp
```
# cd /etc/puppetlabs/code/environments/production/manifests
# vi media.pp
node 'stapp02.stratos.xfusioncorp.com' {
}

file { '/opt/itadmin/media.txt':
     content => 'Welcome to xFusionCorp Industries!',
     mode => '0755',
}
```
- Save and exit the file

- Validate the file with puppet parser
```
# puppet parser validate media.pp 
```

-  Login to app server, switch to the root user and execute the command to apply changes
```
$ sudo su -
# sudo puppet agent -tv
```

- Verify the file is created with the correct content and file permissions
```
# ls -l /opt/itadmin/media.txt 
# cat /opt/itadmin/media.txt 
```