Mysql roles
=====

- Cài đặt và config MySQL
- Hỗ trợ: Ubuntu (14.04, 16.04)


Role Variables
--------------

Các biến nằm trong file defaults/main.yml:
```
---
mysql_user_home: /root
mysql_root_username: root

# MySQL connection settings.
mysql_port: "3306"
mysql_bind_address: '0.0.0.0'
mysql_datadir: /var/lib/mysql
mysql_pid_file: /var/run/mysqld/mysqld.pid

# Slow query log settings.
mysql_slow_query_log_enabled: yes
mysql_slow_query_log_file: /var/log/mysql-slow.log
mysql_slow_query_time: 2

mysql_key_buffer_size: "16MB"
mysql_max_allowed_packet: "16MB"
mysql_max_connections: 150
mysql_myisam_recover: "BACKUP"
mysql_query_cache_size: "16MB"
mysql_query_cache_limit: "1MB"

# Other settings.
mysql_wait_timeout: 28800
overwrite_global_mycnf: True
mysql_root_password_update: no
mysql_enabled_on_startup: yes


mysql_mysqldump_max_allowed_packet: "16MB"
mysql_config_include_files: /etc/mysql/conf.d/

# Logging setting
mysql_log: ""
mysql_log_error: /var/log/mysql.err
mysql_syslog_tag: mysql
```

Các biến theo OS nằm trong các folder vars

vars/Debian.yml
```
---
__mysql_daemon: mysql
__mysql_packages:
  - mysql-common
  - mysql-server
__mysql_slow_query_log_file: /var/log/mysql/mysql-slow.log
mysql_config_file: /etc/mysql/my.cnf
mysql_config_include_dir: /etc/mysql/conf.d
mysql_socket: /var/run/mysqld/mysqld.sock
```

Example Playbook
----------------
```
- name: install and configure mysql 
  hosts: mysql 
  remote_user: root
  roles:
    - mysql 
  vars:
    - mysql_root_password: root
```