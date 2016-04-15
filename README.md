Mysql
=====
Install and configure mysql database server.

This role adds the official mysql repository, but leaves it disabled.

Select the version to install with `mysql_version`. You should also change the root password, the default is `mysql`.

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
Licensed under [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

Author Information
------------------
Luis Gracia <luis.gracia@ebi.ac.uk>
