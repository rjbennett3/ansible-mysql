Mysql
=====
Install and configure MySQL/MariaDB database servers.

This role adds the official MySQL repository, but leaves it disabled. Alternatively users can provide a custom list of repositories (`mysql_repos`) and packages (`mysql_packages`) to install. For example, to install MariaDB once can provide the following:

```
mysql_version: '10.3'

mysql_repos:
  - name: mariadb
    description: MariaDB
    baseurl: 'http://yum.mariadb.org/{{mysql_version}}/centos7-amd64'
    gpgkey: 'https://yum.mariadb.org/RPM-GPG-KEY-MariaDB'
    gpgcheck: yes

mysql_packages:
  - MariaDB-server
  - MySQL-python
```

When providing a custom list of packages, don't forget to add `MySQL-python` for Ansible modules to work.

Select the version to install with `mysql_version`. You should also change the root password with `mysql_root_password`, the default is `mysql`.

The installation is secured following best practices found in the MySQL manual, i.e. removing anonymous users and the test database. This step can be skipped by setting `mysql_secure: false`. Note securing the databases has only been tested on MySQL 5.6.

Multiple databases can be configured through `mysql_databases` list. Databases, users and grants will be generated based on this list (see `default/main.yml` for options).

A local backup cron job can installed under the `mysqlbck` user. The template backup script is located in `templates/backup_all.sh.j2`. Note the default behavior has changed in v2.0.0, users need to explicitly activate this options with `mysql_backup: true`.

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
- Test secure installation for MySQL 5.7+ and MariaDB.
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
