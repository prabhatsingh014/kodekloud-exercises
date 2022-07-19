- Create a manifest file with .pp extension at the path /etc/puppetlabs/puppet/code/environment/production/manifests/ on the puppet server i.e. jump_host
```
$ sudo vi media.pp
node 'stapp03.stratos.xfusioncorp.com' {
}

package { 'httpd':
  ensure => 'installed',
}
```
- Save and exit the file.

- Ensure the puppetserver and puppet services are running on the puppet master and puppet agent nodes by running the following commands.
```
$ sudo systemctl status puppetserver # On puppet server node
$ sudo systemctl status puppet  # On puppet agent node
```

- If puppet agent node is unable to connect to the puppet server, check the hostname "puppet" is defined against the puppet server IP.
```
$ cat /etc/hosts
```

- Restart the puppet agent service
```
$ sudo systemctl restart puppet
```

- Run the following command to apply the changes on the agent node as defined in the manifest file.
```
$ sudo puppet agent -tv   #If logged in from non-root user, ensure to put sudo with the command.
```