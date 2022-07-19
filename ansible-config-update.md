- Ansible Config File Update
```
ansible.cfg
```

- Uncomment following line to enable SSH on the required user.
```
#remote_user: <username>
```

- Save the file

### You can also test this by following steps:
- Setup passwordless connectivity between ansible controller and target nodes by copying public key of ansible controller node to target users' authorised_keys.
- Setup the ansible inventory with the hostnames or IPs of the target machine.
- Run below command to verify the user which is being used for SSH towards target machines and run tasks.

```
# ansible -m ping all -vvvv
```

- The output will show the user.