- Login to jump host as root user
- Create puppet manifest file under the directory using vi editor
```
# cd /etc/puppetlabs/code/environment/production/manifests/
# vi cluster.pp 
node 'stapp03.stratos.xfusioncorp.com' {
    include installnginx
}

class installnginx {
    package {'nginx':
      ensure => installed,
    }
    service {'nginx':
      ensure => running,
      enable => true,
    }
}
```
- Save and exit the file

- Login to application server 3 as root user
- Execute the command to immplement the changes
```
# puppet agent -tv
```

- Verify if the service is installed and running on application server 3
```
# systemctl status nginx
```