Deploy osTicket on Amazon Linux 2
=================================

Deploy OSTicket via Ansible

## Directory Structure

```
├── db.yml
├── dev
├── group_vars
│   ├── all.yml
│   ├── db.yml
│   └── web.yml
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