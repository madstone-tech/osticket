Deploy osTicket on Amazon Linux 2
=================================

This playbook sets out to install 

* latest version of osticket
* php 7.2
* nginx
* mariadb 10.2

List of Roles
=========

* common
* db
* nginx
* web

Playbook description
====================

| playbook  | roles            | description                                        |
| --------- | ---------------- | -------------------------------------------------- |
| `db.yml`  | common,db        | runs common role and db                            |
| `web.yml` | common,web,nginx | runs common, installs osticket and configure nginx |

Inventory files
===============

| inventory | purpose                 |
| --------- | ----------------------- |
| dev       | dev environnment        |
| site      | production environnment |

*IPs for servers should be updated to reflect your environment* 


Requirements
------------

* Amazon-Linux-2
* Vagrant and Virtualbox if unsing Vagrantfile
* Ansible 2.8+


Role Variables
--------------

variables are found in `group_vars/all.yml`

| Role variable              | default                            | description                           |
| -------------------------- | ---------------------------------- | ------------------------------------- |
| `_db_user_`                | `osticket_user`                    | database user                         |
| `_db_pass_`                | `osticket_password`                | database password                     |
| `_db_name_`                | `osticket_db`                      | database name                         |
| `_db_host_`                | `192.168.44.11`                    | database host                         |
| `domain_url`               | `support.madst.one`                | domain url                            |
| `_ssl_cert_directory_`     | `/etc/ssl/certs`                   | certificate directory                 |
| `_ssl_cert_key_directory_` | `/etc/ssl/private`                 | certificate key directory             |
| `_ssl_cert_csr_directory_` | `/etc/ssl/csr`                     | certificate signing request directory |
| `_ssl_cert_path_`          | `/etc/ssl/certs/ssl-cert.crt`      | path to certificate                   |
| `_ssl_cert_key_`           | `/etc/ssl/private/ssl-privkey.pem` | path to certificate private key       |
| `_ssl_cert_csr_`           | `/etc/ssl/csr/ssl-csr.csr`         | path to certificate signing request   |

modify the variable to suit your environment

directory structure
===================


```
├── db.yml
├── dev
├── group_vars
│   ├── all.yml
├── production
├── README.md
├── roles
│   ├── common
│   │   ├── handlers
│   │   │   └── main.yml
│   │   └── tasks
│   │       └── main.yml
│   ├── db
│   │   ├── handlers
│   │   │   └── main.yml
│   │   └── tasks
│   │       └── main.yml
│   ├── nginx
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── tasks
│   │   │   └── main.yml
│   │   └── templates
│   │       └── osticket.conf.j2
│   └── web
│       ├── files
│       │   ├── php.ini
│       │   └── www.conf
│       ├── handlers
│       │   └── main.yml
│       └── tasks
│           └── main.yml
├── Vagrantfile
└── web.yml
```

Dependencies
------------

If running this playbook Vagrant, Vagrant and Virtualbox need to be installed


License
-------

BSD

Author Information
------------------

Andhi Jeannot
MADSTONE TECHNOLOGY, inc
https://madstone.io

https://github.com/madstone-tech