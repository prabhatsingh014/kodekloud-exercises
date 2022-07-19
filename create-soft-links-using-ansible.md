- Verify if inventory file consists of host entries
```
$ cat inventory
```

- Create playbook.yml using vi editor to accomplish the tasks given in the question
```
$ vi playbook.yml
---
- hosts: stapp01
  become: yes
  tasks:
    - name: Create a file blog.txt
      file:
        path: /opt/devops/blog.txt
        state: touch
        owner: tony
        group: tony

- hosts: stapp02
  become: yes
  tasks:
    - name: Create a file story.txt
      file:
        path: /opt/devops/story.txt
        state: touch
        owner: steve
        group: steve

- hosts: stapp03
  become: yes
  tasks:
    - name: Create a file media.txt
      file:
        path: /opt/devops/media.txt
        state: touch
        owner: banner
        group: banner

- hosts: all
  become: yes
  tasks:
    - name: Create symbolic link
      file:
        src: /opt/devops
        dest: /var/www/html
        state: link
```
- Save and exit the file

- Dry-run the playbook if all changes are implemented correctly
```
$ ansible-playbook -i inventory playbook.yml --check
```

- Execute the following command to run the playbook
```
$ ansible-playbook -i inventory playbook.yml
```

- Verify if all files are created with correct ownership
```
$ ansible all -m shell -a 'ls -l /opt/devops' -i inventory 
```

- Verify if the softlinks are created correctly
```
$ ansible all -m shell -a 'ls -l /var/www' -i inventory
```