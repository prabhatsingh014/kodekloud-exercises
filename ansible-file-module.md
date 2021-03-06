- Create the inventory with the host details of all application servers
```
$ vi ~/playbook/inventory
stapp01 ansible_host=172.16.238.10 ansible_user=tony ansible_password=Ir0nM@n
stapp02 ansible_host=172.16.238.11 ansible_user=steve ansible_password=Am3ric@
stapp03 ansible_host=172.16.238.12 ansible_user=banner ansible_password=BigGr33n
```
- Save and exit the file

- Create playbook with the task that is required to be performed.
```
$ vi ~/playbook/playook.yml
- hosts: all
  become: yes
  tasks:
  - name: Create a file
    file:
      path: /tmp/opt.txt
      state: touch
      owner: "{{ ansible_user }}"
      group: "{{ ansible_user }}"
      mode: 0655
```
- Save and exit the file

- Edit the /etc/ansible/ansible.cfg file to default inventory to the path /home/thor/playbook/inventory
```
$ sudo vi /etc/ansible/ansible.cfg
inventory = /home/thor/playbook/inventory
```
- Save and exit the file

- Dry run the playbook which was created by executing following command
```
$ cd /home/thor/playbook
$ ansible-playbook -i inventory playbook.yml --check
```

- If all looks good, run the playook to implement the changes
```
$ ansible-playbook -i inventory playbook.yml
```

- Execute following command to verify the changes implemented on all application servers.
```
$ ansible all -m shell -a 'ls -l /tmp/opt.txt' -i inventory
```