- Create playbook.yml on the jump host at the location /home/thor/ansible
```
$ vi /home/thor/ansible/playbook.yml
- hosts: stapp01
  become: yes
  tasks:
  - name: Create blog.txt file
    file:
      path: /opt/security/blog.txt
      owner: root
      group: root
      state: touch

  - name: Set acl on blog.txt on app server 1
    acl:
      path: /opt/security/blog.txt
      etype: group
      entity: tony
      permissions: r
      state: present

- hosts: stapp02
  become: yes
  tasks:
  - name: Create story.txt file
    file:
      path: /opt/security/story.txt
      owner: root
      group: root
      state: touch

  - name: Set acl on story.txt on app server 2
    acl:
      path: /opt/security/story.txt
      etype: user
      entity: steve
      permissions: rw
      state: present

- hosts: stapp03
  become: yes
  tasks:
  - name: Create media.txt file
    file:
      path: /opt/security/media.txt
      owner: root
      group: root
      state: touch

  - name: Set acl on media.txt on app server 3
    acl:
      path: /opt/security/media.txt
      etype: group
      entity: banner
      permissions: rw
      state: present
```
- Save and exit the file

- Execute following command to implement the required changes on all app servers
```
$ cd /home/thor/ansible
$ ansible-playbook -i inventory playbook.yml
```

- Execute following command to check the file has been created on all app server as per requirement
```
$ ansible all -m shell -a 'ls -l /opt/security' -i inventory
```

- Execute following command to check the acl on the file on all app servers
```
$ ansible stapp01 -m shell -a 'getfacl /opt/security/blog.txt' -i inventory
$ ansible stapp02 -m shell -a 'getfacl /opt/security/story.txt' -i inventory
$ ansible stapp03 -m shell -a 'getfacl /opt/security/media.txt' -i inventory
```