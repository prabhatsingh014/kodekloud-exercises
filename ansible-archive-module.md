- Create playbook.yml under /home/thor/ansible directory using vi editor and with the following content

```
$ vi playbook.yml

- hosts: all
  become: yes
  tasks:
  - name: Create archive on application server
    archive:
      path: /usr/src/finance/
      dest: /opt/finance/media.tar.gz
      owner: "{{ ansible_user }}"
      group: "{{ ansible_user }}"
```

- Save and exit the file

- Execute the following command to check if the playbook will do changes as required
```
$ ansible-playbook -i inventory playbook.yml --check
```

- If it works as required, execute the following command to apply the changes
```
$ ansible-playbook -i inventory playbook.yml
```

- Execute following command to check if the archive is created with right permission and ownership
```
$ ansible all -m shell -a 'ls -l /opt/finance' -i inventory
```