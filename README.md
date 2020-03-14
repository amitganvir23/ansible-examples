# ansible-examples


## Run below command to create ansible role directory structure
$ ansible-galaxy roles/deploy init
## To list all the contents of that directory
$ ll roles/
$ ls -R roles/
$ ls roles/deploy

## Create a python sample file
$ vim roles/deploy/files/hi.py

#!/usr/bin/python
print"Hello World"

:wq
##

[ec2-user@ip-172-31-82-132 ~]$ cat amit.yml
---
- hosts: web
  user: ec2-user
  sudo: true
  tasks:
  roles:
    - deploy
[ec2-user@ip-172-31-82-132 ~]$


[ec2-user@ip-172-31-82-132 ~]$ cat roles/deploy/tasks/main.yml
---
# tasks file for roles/deploy
- name: Copying python file
  copy:
    src: hi.py
    dest: /tmp/hi.py
    mode: 777

- name: executing code to deploy
  shell: "/tmp/hi.py"
[ec2-user@ip-172-31-82-132 ~]$

ansible-playbook -i myhost amit.yml --private-key .ssh/ec2_private.key -vvv
