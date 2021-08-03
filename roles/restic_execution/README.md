# restic_backup

Runs a restic backup job in a remote host.

## Requirements

Restic must be installed in the inventory instances.

## Role Variables

|---|---|
|folders |List of folders to backup (required) |
|restic_repository |The path to the restic repository (required) |
|restic_password |Repository password (required) |
|remote_pre_command |Shell command to be executed in the remote instance before restic |
|remote_post_command |Shell command to be executed in the remote instance after restic |
|local_pre_command| Shell command to be executed in the local machine before anything else |
|local_post_command| Shell command to be executed in the local machine after everything else |
|restic_forget| Flag to determine if restic forget with prune is executed |
|keep_weeky| Keep 1 snapshot per week for N weeks |
|keep_monthly| Keep 1 snapshot per month for N months |
|keep_yearly| Keep 1 snapshot per year for N years |
|keep_last| How many snapshots to keep. If this is defined it will have precedence over the weekly, monthly and yearly |

## Dependencies

None.

## Example Playbook

- hosts: restic_backup
  roles:
  - restic_backup:
    vars:
      folders: "/var/ssh"
      restic_repository: "/home/user/restic"
      restic_password: "password"
      remote_pre_command: "systemctl stop nginx"
      remote_post_command: "systemctl start nginx"
      local_pre_command: "ls"
      local_post_command: "ls"
      restic_forget: yes
      keep_weekly: 5
      keep_monthly: 12
      keep_yearly: 50
      keep_last: ""

## License

None.
