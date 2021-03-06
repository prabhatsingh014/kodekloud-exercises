- Create manifest file using vi editor on jump host using root user
```
# vi blog.pp

class ssh_node1 {
  ssh_authorized_key { 'jump_host.stratos.xfusioncorp.com':
  ensure => present,
  user   => 'tony',
  type   => 'ssh-rsa',
  key    => 'AAAAB3NzaC1yc2EAAAADAQABAAABAQC8vE9Psh18BBbtuiPW57vP/lYkNdxtpqeWBFiEojIL8hJSqB4ePJK0sbGw2cqCGfDEjS1dbzf2Y4rAfN1PDLho4Y2aPCRmF7Sz9bjXNk9L7quznpxzm7CauWjTFKxO/ZXhSgERMqTUft3S/89Z5X0H4UzUaKuHmAl8uABBlNbDaTPnjM60uGqct9MfPv5DXCaOJkQls++YHW+v3Fo50/anE1ZQ+ghM7QkEdI11rhFfIp5YY/obRItKjAenFOrqOKYOBlGpyAHO6Fj+vBmtLGBzytWhU+SoCJPuPBYxvfibY6u+IOkIVdU99rqbkl01M4YSOcgSbrB3iBYKtG6m6ZVX',
  }
}
class ssh_node2 {
  ssh_authorized_key { 'jump_host.stratos.xfusioncorp.com':
  ensure => present,
  user   => 'steve',
  type   => 'ssh-rsa',
  key    => 'AAAAB3NzaC1yc2EAAAADAQABAAABAQC8vE9Psh18BBbtuiPW57vP/lYkNdxtpqeWBFiEojIL8hJSqB4ePJK0sbGw2cqCGfDEjS1dbzf2Y4rAfN1PDLho4Y2aPCRmF7Sz9bjXNk9L7quznpxzm7CauWjTFKxO/ZXhSgERMqTUft3S/89Z5X0H4UzUaKuHmAl8uABBlNbDaTPnjM60uGqct9MfPv5DXCaOJkQls++YHW+v3Fo50/anE1ZQ+ghM7QkEdI11rhFfIp5YY/obRItKjAenFOrqOKYOBlGpyAHO6Fj+vBmtLGBzytWhU+SoCJPuPBYxvfibY6u+IOkIVdU99rqbkl01M4YSOcgSbrB3iBYKtG6m6ZVX',
  }
}
class ssh_node3 {
  ssh_authorized_key { 'jump_host.stratos.xfusioncorp.com':
  ensure => present,
  user   => 'banner',
  type   => 'ssh-rsa',
  key    => 'AAAAB3NzaC1yc2EAAAADAQABAAABAQC8vE9Psh18BBbtuiPW57vP/lYkNdxtpqeWBFiEojIL8hJSqB4ePJK0sbGw2cqCGfDEjS1dbzf2Y4rAfN1PDLho4Y2aPCRmF7Sz9bjXNk9L7quznpxzm7CauWjTFKxO/ZXhSgERMqTUft3S/89Z5X0H4UzUaKuHmAl8uABBlNbDaTPnjM60uGqct9MfPv5DXCaOJkQls++YHW+v3Fo50/anE1ZQ+ghM7QkEdI11rhFfIp5YY/obRItKjAenFOrqOKYOBlGpyAHO6Fj+vBmtLGBzytWhU+SoCJPuPBYxvfibY6u+IOkIVdU99rqbkl01M4YSOcgSbrB3iBYKtG6m6ZVX',
  }
}

node stapp01.stratos.xfusioncorp.com {
  include ssh_node1
}
node stapp02.stratos.xfusioncorp.com {
  include ssh_node2
}
node stapp03.stratos.xfusioncorp.com {
  include ssh_node3
}
```
- Save and exit the file

- Login to application server 1 with root user
- Execute the command to apply the changes
```
# puppet agent -tv
```

- Once manifest is applied, try login to application server from thor user on the jump host to sudo user of app server
```
$ ssh tony@stapp01
```

- You should be able to login without asking for password