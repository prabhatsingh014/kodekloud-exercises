- Create the playbook.yaml to replace the string on all app servers using vi editor
```
$ vi playbook.yaml
---
- hosts: all
  become: yes
  tasks:
  - name: replace string on app server1
    replace:
      path: /opt/security/blog.txt
      regexp: 'xFusionCorp'
      replace: 'Nautilus'
    when: inventory_hostname == "stapp01"

  - name: replace string on app server2
    replace:
      path: /opt/security/story.txt
      regexp: 'Nautilus'
      replace: 'KodeKloud'
    when: inventory_hostname == "stapp02"

  - name: replace string on app server3
    replace:
      path: /opt/security/media.txt
      regexp: 'KodeKloud'
      replace: 'xFusionCorp Industries'
    when: inventory_hostname == "stapp03"
```
- Save and exit the file

- Execute the playbook using the command
```
$ ansible-playbook -i ~/playbooks/inventory playbook.yaml
```

- Verify the string has been replaced correctly on all app servers using the command
```
$ ansible all -m shell -a 'cat /opt/security/*.txt' -i ~/playbooks/inventory
```