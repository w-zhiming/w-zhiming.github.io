# Gitlab backup & restore

```bash
## Bakcup, store at '/var/opt/gitlab/backups'
gitlab-rake gitlab:backup:create

## shedule task, backup everyday 5:00
0 5 * * * /opt/gitlab/bin/gitlab-rake gitlab:backup:create

## backup config, as below.
[root@localhost init.d]# cd /etc/gitlab/
[root@localhost gitlab]# ls
gitlab.rb  gitlab-secrets.json  trusted-certs

## before restore gitlab, you must stop data link service.
gitlab-ctl stop unicorn
gitlab-ctl stop sidekiq

## see status.
gitlab-ctl status

## restore from backup file.
gitlab-rake gitlab:backup:restore BACKUP=1466811825

# restart.
gitlab-ctl restart

```
