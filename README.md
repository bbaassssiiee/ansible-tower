# TOWER ING
Ansible playbooks for installing Ansible Tower (version 3.0) in corporate environment.

## Installing Ansible Tower on a standalone machine
**You must be able to sudo!**

Install Ansible Tower on your server/workstation, single-instance mode:

```
$ ./deploy.yml
```

## Installing Ansible Tower with remote database
Machine A will be the web server.
Machine B will be the postgre database server.

1. Edit ansible.cfg, change hostfile to point to external_db.ini
```
hostfile = external_db.ini
```
2. Modify external_db.ini to your liking

3. Deploy tower:
```
$ ./deploy.yml
```

## Installing Ansible Tower with remote database
Machine A will be the primary web server.
Machine B will be the primary postgre database server.
Machine C will be the secondary web server.
Machine D will be the secondary postgre database server.
1. Edit ansible.cfg, change hostfile to point to intranet.ini
```
hostfile = intranet.ini
```
2. Modify intranet.ini to your liking

3. Deploy tower:
```
$ ./deploy.yml
```
