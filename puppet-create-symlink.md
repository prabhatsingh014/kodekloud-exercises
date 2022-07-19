- Create a file at the location of manifest with the name blog.txt and with following content on the puppet server
- Make sure to do the task using either root user or sudo access
```
$ vi /etc/puppetlabs/code/environment/production/manifests/blog.pp
class symlink {
  file { '/opt/sysops':
    ensure => 'link',
    target => '/var/www/html',
  }
  file { '/opt/sysops/story.txt':
    ensure => 'present'
  }
}

node 'stapp01.stratos.xfusioncorp.com' {
  include symlink
}
```
- Save the file and exit

- Validate the manifest file by running following command on the puppet server
```
$ puppet parser validate blog.pp
```

- Logon to the application server (i.e. puppet agent node) and run the following command test and apply the changes
```
$ puppet agent -tv
```

- Check if the link and file is created and present at the respective location on the puppet agent
```
$ ls -l /var/www/html
$ ls -l /opt/sysops
```