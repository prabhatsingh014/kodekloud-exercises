- Check the inventory file placed at /home/thor/ansible/inventory
- It must have ansible_user and ansible_ssh_pass along with the target nodes IP details.

- Create a playbook /home/thor/ansible/playbook.yml
```
$ vi /home/thor/ansible/playbook.yml
---
- hosts: all
  become: yes
  tasks:
  - name: Copy blog file
    copy:
      src: "/usr/src/sysops/blog.txt"
      dest: "/opt/sysops"
      owner: tony
      group: tony
      mode: 0644
    register: stapp01host
    when: inventory_hostname == "stapp01"

  - name: Copy story file
    copy:
      src: "/usr/src/sysops/story.txt"
      dest: "/opt/sysops"
      owner: steve
      group: steve
      mode: 0644
    when: inventory_hostname == "stapp02"

  - name: Copy media file
    copy:
      src: "/usr/src/sysops/media.txt"
      dest: "/opt/sysops"
      owner: banner
      group: banner
      mode: 0644
    when: inventory_hostname == "stapp03"
```    
- Save the exit the file

- Dry run the ansible playbook using following command.
```
$ ansible-playbook -i inventory playbook.yml --check
```

- Run the ansible playbook using following command.
```
$ ansible-playbook -i inventory playbook.yml
```

Note: Tasks asks to use ansible_nodename in the output of the facts gathered by the ansible. But you can also use ansible inbuilt variable "inventory_hostname" in the when conditions.