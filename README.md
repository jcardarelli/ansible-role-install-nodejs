# ansible-role-install-nodejs
Ansible role to install nodejs

Based on these instructions:
- https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions-enterprise-linux-fedora-and-snap-packages
- https://github.com/nodesource/distributions/blob/master/README.md#deb

## Requirements

Ansible v2.8+ for github_release module to have anonymous access to query repository info:
- https://github.com/ansible/ansible/issues/45391

Setup module must be run with playbook to gather facts in the `ansible_facts` variable. This is the default, so if you set `gather_facts: no` in your playbook, it will break this role since variables such as `"{{ ansible_distribution_release }}"` will not be available.

## Role Variables

## Dependencies

## Example Playbook

Please see `example-playbook.yml`

## License

BSD

## Author Information

https://github.com/jcardarelli/
