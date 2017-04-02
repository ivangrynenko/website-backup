## Backup website files and mysql databases role

Available variables, they could be set in group_vars/all.yml file in your
playbook:

By default the files are backed up into user home folder and the backup 
directories are created automatically. Set the username here:
`ivrh_default_backup_user_username: ubuntu`

Backup location definitions (taking username as a variable):
`ivrh_mysql_backup_location: "/home/{{ ivrh_default_backup_user_username }}/mysql_backup"`
`ivrh_mysql_daily_backup_location: "/home/{{ ivrh_default_backup_user_username }}/mysql_backup_daily"`

How many days of backups to retain for
`ivrh_mysql_days_to_retain_backups_for: 30`

Username and password to use with mysqldump:
`mysql_user_name: root`
`mysql_root_password: root`

Set this as the source path where your website files are stored.
`ivrh_source_backup_path: "/var/www/html"`

Set this variable to path where backup of website files will be located
`ivrh_website_backup_destination: "/home/{{ ivrh_default_backup_user_username }}/backup_website"`

Path where to upload mysql backup script
`ivrh_mysql_backup_script_location: "/usr/local/bin/backupmysql"`

## Example playbook
```
- name: Backup all websites in all servers
  hosts: webservers
  remote_user: ubuntu
  sudo: yes
  pre_tasks:
    - set_fact: ivrh_default_backup_user_username=yourcustomusername

  vars_files:
  roles:
    - { role: website-backup }
```
