- Ensure the puppetserver and puppet services are running on the jump host and database node respectively.
- Ensure that the /etc/hosts file contains the fqdn and hostname of puppet agent and puppet server

- Install the puppet-yum module on the puppetserver node i.e. jump host.
```
$ sudo puppet agent module install puppet-yum
```

- Create a manifest file official.pp at the location /etc/puppetlabs/code/environment/production/manifests/ on the jump host
```
$ vi official.pp
node 'stdb01.stratos.xfusioncorp.com' {
  include mysql_database
}

class mysql_database {
  package { 'mariadb-server':
    ensure => 'installed',
  }
  service { 'mariadb':
    ensure => 'running',
  }
  mysql::db { 'kodekloud_db2':
    user     => 'kodekloud_top',
    password => 'TmPcZjtRQx',
    host     => 'localhost',
    grant    => ['SELECT', 'UPDATE'],
  }
}
```
- Save and exit the file

- On the puppet agent node i.e. DB server, run the following command to apply the manifest.
```
$ sudo puppet agent -tv
```

- Once the changes are applied, verify the changes using below commands on the puppet agent node.
```
$ mysql
# mariadb> \r kodekloud_db2     // You should be able to connect to the database.
# mariadb:[kodekloud_db2]> select user from mysql.user;     // User created using puppet manifest should be displayed.
```