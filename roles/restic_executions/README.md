# restic_backup

Runs one or many restic backup jobs in a remote host.

## Requirements

It invokes role restic_backup which lives inside the same playbook so... all ok.

## Role Variables

|---|---|
|jobs |A list of dictionaries in which each item describes a backup job. |
|group |Execute only jobs belonging to this group (optional) |

Example:

```yaml
restic_backup_jobs:
- folders:
    - /var/www/dokuwiki
    - /etc/ssl
    - /etc/nginx
  restic_repository: /home/nununo/restic
  restic_password: "xxx"
  remote_pre_command: "/bin/systemctl stop nginx"
  remote_post_command: "/bin/systemctl start nginx"
  group: barril
```

Please see `restic_backup`'s README for details on the possible variables for each job.

## Dependencies

None.

## Example Playbook

- hosts: restic_backup
  gather_facts: no
  roles:
  - role: restic_backups
    vars:
      jobs: "{{ restic_backup_jobs }}
      group: barril

## License

None.
