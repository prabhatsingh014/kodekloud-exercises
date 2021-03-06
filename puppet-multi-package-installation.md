- Create media.pp manifest file at the location /etc/puppetlabs/code/environments/production/manifests on the jump host server
```
# vi /etc/puppetlabs/code/environments/production/manifests/media.pp

node 'stapp03.stratos.xfusioncorp.com' {
    include multi_package_node
  }
  
class multi_package_node {
  package {'net-tools':
    ensure => 'installed',
  }
  package {'unzip':
    ensure => 'installed',
  }
}
```
- Save and exit the file

- Verify the puppetserver and puppet service status on jump host and application server using the command
```
# systemctl status puppetserver
# systemctl status puppet
```

- There could be an error related to reaching puppet server in the output of puppet service status on the application server
- To resolve the issue, update the /etc/hosts file on jump host and application server to include "puppet" against the jump host entry

- Once /etc/hosts file is updated, restart the puppetserver service on the jump host
```
# systemctl restart puppetserver
```

- Then restart the puppet service on the application server
```
# systemctl restart puppet
```

- On application server, execute the command to apply the puppet manifest
```
# puppet agent -tv
```

- Once done, execute the command to verify if all packages are installed
```
# rpm -qa | egrep 'net-tools|unzip'
```