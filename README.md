Mysql
=====
Install and configure mysql database server.

This role adds the official mysql repository, but leaves it disabled. It also adds MySQL Python to use Ansible modules.

Select the version to install with `mysql_version`. You should also change the root password, the default is `mysql`.

The installation is secure following best practices found in the MySQL manual, ie removing anonymous users and the test database.

Multiple databases can be configured through `mysql_databases` list. Databases, users and grants will be generated based on this list (see `default/main.yml` for options).

A local backup cron job can installed under the `mysqlbck` user when setting `mysql_backup: true`. The template backup script is located in `templates/backup_all.sh.j2`.

Requirements
------------
See `meta/main.yml`.

Role Variables
--------------
See `default/main.yml`.

Dependencies
------------
None.

Example Playbook
----------------
Example:
```
- hosts: servers
  roles:
    - { role: mysql, mysql_version: 5.6, mysql_root_password: mypassword }
```

TODO
----
- Secure installation for 5.7.
- Backup should be optional.
- Creating backup user does not work if account is already in ldap.
- Restrict backup user privileges, i.e `SELECT,RELOAD,FILE,SUPER,"LOCK TABLES","SHOW VIEW","SHOW DATABASES"`.

Licence
-------
Released under the [MIT license](https://opensource.org/licenses/MIT).

Author Information
------------------
Luis Gracia while at [EMBL-EBI](http://www.ebi.ac.uk/):
- luis.gracia [at] ebi.ac.uk
- GitHub at [luisico](https://github.com/luisico)
- Galaxy at [luisico](https://galaxy.ansible.com/luisico)
