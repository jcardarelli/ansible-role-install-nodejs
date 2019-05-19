# ansible-role-install-nodejs
Ansible role to install nodejs

Based on these instructions:
- https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions-enterprise-linux-fedora-and-snap-packages
- https://github.com/nodesource/distributions/blob/master/README.md#deb


## Quick start:

#### Setup ansible virtualenv
```
virtualenv --system-site-packages --python python3 ~/.virtualenvs/ansible3
```

#### Activate ansible virtualenv
```
source ~/.virtualenvs/ansible3/bin/activate
```

#### Install ansible into virtualenv
```
pip install ansible
```

#### Clone this repo to your ansible roles directory
```
git clone https://github.com/jcardarelli/ansible-role-install-nodejs.git $HOME/ansible/roles/install-nodejs
```

#### To install on localhost
```
cd $HOME/ansible/roles/install-nodejs
ANSIBLE_CONFIG=~/ansible/ansible.cfg ansible-playbook example-playbook.yml --limit localhost --ask-become-pass
```

## Requirements

1. Ansible v2.8+ for github_release module to have anonymous access to query repository info: https://github.com/ansible/ansible/issues/45391

1. Setup module must be run with playbook to gather facts in the `ansible_facts` variable. This is the default, so if you set `gather_facts: no` in your playbook, it will break this role since variables such as `"{{ ansible_distribution_release }}"` will not be available.

1. This role assumes that you're using a virtualenv setup like so:
```
$ virtualenv --system-site-packages --python python3 ~/.virtualenvs/ansible3
Running virtualenv with interpreter /usr/bin/python3
Using base prefix '/usr'
New python executable in /home/stressed/.virtualenvs/ansible3/bin/python3
Also creating executable in /home/stressed/.virtualenvs/ansible3/bin/python
Installing setuptools, pip, wheel...done.
```

## Role Variables

## Dependencies

- Module `github_release` requires `github3.py`. This role contains a task that will install this pip package into Ansible's virtualenv. Specify your Ansible virtualenv with the variable `"{{ ansible_venv }}"`.


## Example Playbook

Please see `example-playbook.yml`

## License

BSD

## Author Information

https://github.com/jcardarelli/
