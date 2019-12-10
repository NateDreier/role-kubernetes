Role Name
=========

This role configures a host with vanilla Docker (meta/main.yml) and vanilla Kubernetes. Below I have described the four important files/directories you need, the kubernetes.yml, requirements.yml and the host file. The command that gets run looks at the requirements file and pulls all the defined roles and installs them into `roles/`, after that your typical `ansible-playbook` command gets run, finally it cleans up everything that was pulled down. Credit for that one goes to a good buddy.

Requirements
------------

My setup is - 
kubernetes.yml
```
---
- hosts: hosts
  gather_facts: true
  become: true

  roles:
    - role-kubernetes
```
requirements.yml
```
- name: role-kubernetes
  src: https://github.com/NateDreier/role-kubernetes
```
hosts
```
[hosts:children]
master-nodes
worker-nodes

[master-nodes]
some.address.or.ip

[worker-nodes]
some.address.or.ip
```

Make sure you have a dir called roles then run the following command:
ansible-galaxy install -r requirements.yml --roles-path roles/ && ansible-playbook -i hosts kubernetes-install.yml -u user -D && rm -rf roles/*


Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
