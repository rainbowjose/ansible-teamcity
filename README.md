

  
ansible-teamcity
=========

ansible-teamcity is an [Ansible](http://ansible.com) role.
Use this role to install [Teamcity](http://www.jetbrains.com/teamcity/) server. Tested on Ubuntu 18.04 with Teamcity 2020.1.5 .

Requirements
------------

1. Ansible 1.4 or higher
2. Ubuntu 18.04
3. Vagrant (optional)
4. PostgreSQL (other RDBMS which Teamcity support)

Role Variables
--------------

## Server
The role has default value that should work without modification unless you want to

Settings for server:

    teamcity_server_version: 2020.1.5

External database settings for server:
| Variable name               | Default value      | Description                |
|-----------------------------|--------------------|----------------------------|
| host                        |  `localhost`       | DB hostname                |
| name                        |  `teamcity`        | DB name                    |
| user                        |  `teamcity`        | DB username                |
| port                        |  `5432`            | DB port                    |

## Agent
Settings for agent:
| Variable name               | Default value      | Description                |
|-----------------------------|--------------------|----------------------------|
| teamcity_agent_server_url   |  `localhost`       | TeamCity Server URL        |
| teamcity_agent_server_port  |  `8111`            | TeamCity Server Port       |
| teamcity_agent_install_dir  |  `/opt/buildAgent` | TeamCity Agent Install Dir |
| teamcity_server_user_name   | `teamcity`         | Teamcity Adminin User      |
| teamcity_server_user_passwd | `teamcity`         | Teamcity Admin Password    |

--------------

You can change variables in 
```roles/teamcity-server/defaults/main.yml```,
```roles/teamcity-agent/defaults/main.yml```
and hosts in ```hosts```



Usage
----------------

### Get the code

```bash
$ git clone git@github.com:rainbowjose/ansible-teamcity.git
```

The code should reside in the roles directory of ansible ( See [ansible documentation](http://www.ansibleworks.com/docs/playbooks.html#roles) for more information on roles ), in a folder jenkins.

### Create vagrant environment
```
cd vagrant
vagrant up
```

### Edit a host file

Following example make ansible aware of the Vagrant box reachable on localhost port 2222.

```bash
$ vi hosts
```

with

```ini
[teamcity-servers]
vagrant@192.168.33.10
[teamcity-agent-servers]
vagrant@192.168.33.11
vagrant@192.168.33.12
vagrant@192.168.33.13
```

### Run the playbook

```bash
$ ansible-playbook playbook.yml -i hosts
```

License
-------

MIT
