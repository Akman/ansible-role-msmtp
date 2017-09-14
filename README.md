# Ansible Role: MSMTP

Installs MSMTP on Linux.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    msmtp_accounts: []

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - Akman.msmtp

*Inside `vars/main.yml`*:

    msmtp_accounts: []

## License

MIT / BSD

## Author Information

This role was created in 2017 by Alexander Kapitman
