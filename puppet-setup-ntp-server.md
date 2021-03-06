- Perform the task as root user to make it easier
- Create the manifest file on the jump host using vi editor
```
# vi /etc/puppetlabs/code/environments/production/manifests/news.puppetlabs

node 'stapp01.stratos.xfusioncorp.com' {
  include ntpconfig
}

class ntpconfig {
  package { 'ntp':
    ensure => 'installed',
  }
  
  file { '/etc/ntp.conf':
    ensure => present
  }->

  file_line { 'ntpserver':
    line => 'server 3.europe.pool.ntp.org iburst',
    path => '/etc/ntp.conf',
  }

}
```

- Install the puppetlabs-stdlib module for using file and file_line modules with puppetlabs
```
# cd /etc/puppetlabs/code/environments/production/modules
# puppet module install puppetlabs-stdlib
```

- Login to application server as root user and execute the command to implement the changes
```
# puppet agent -tv
```

- Verify if the entry has been populated in the ntp.conf as asked in the question
```
# cat /etc/ntp.conf
```