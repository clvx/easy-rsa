EASY-RSA
=========

Ansible role to generate an OpenVPN PKI with easy-rsa

Requirements
------------

- Ansible >= 2.1
- Ubuntu >= 16.04

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

| Variables | Default | Description |
|---------------|--------------------|-----------------|
| deploy_key_dir |  "{{ playbook_dir }}/files }}" |  Where keys will be stored |
| easy_rsa_dir |  /usr/share/easy-rsa | Path to easy-rsa executables |
| easy_rsa_keydir |  "{{ deploy_key_dir }}" | Where keys will be stored |
| easy_rsa_key_size |  2048 | key size |
| easy_rsa_key_country |  "PE" | Country |
| easy_rsa_key_province |  "LIMA" | Province |
| easy_rsa_key_city |  "LIMA" | City |
| easy_rsa_key_org |  "BAR" | Organization }
| easy_rsa_key_email |  "foo@example.com" | email |
| easy_rsa_key_ou |  "IT" | Organization Unit |
| easy_rsa_force_pki |  "False" | If a pki exists, deletes everything and creates a new one |
| easy_rsa_inventory |  True | Use inventory names for pki files associated with `lab-servers` and `lab-clients group` |
| groups['lab-servers'] | your invetory servers  | When `easy_rsa_inventory` is `True`, *Inventory group* which list all servers | 
| groups['lab-clients'] | your inventory clients  | When `easy_rsa_inventory` is `True`, *Inventory group* which list all clients | 
| server_list |  [] | When `easy_rsa_inventory` is `False`, it will use these servers instead | 
| client_list |  [] | When `easy_rsa_inventory` is `False`, it will use these clients instead | 

Dependencies
------------

None

Example Playbook
----------------

This playbook works in 2 ways:

1. You can build and mantain your pki with Ansible using inventory hosts to refer your keys and certs.

Inventory:

    [lab-clients]
    localhost

Playbook:

    - hosts: lab-clients
      roles:
         - clvx.easy-rsa

2. You can define your own clients and variables with `server_list` and `client_list`.

Playbook:

    - hosts: lab
      vars:
        - server_list:
            - server1
            - server2
        - client_list:
            - client1
            - client2
      roles:
        - clvx.easy-rsa

License
-------

GPLv3

Author Information
------------------

Luis Michael Ibarra

clvx: irc, twitter, reddit, etc.
