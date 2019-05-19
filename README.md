# install-nodejs

Based on these instructions:
- https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions-enterprise-linux-fedora-and-snap-packages
- https://github.com/nodesource/distributions/blob/master/README.md#deb

## Really Quick start for localhost installation:
```
virtualenv --system-site-packages --python python3 ~/.virtualenvs/ansible3
source ~/.virtualenvs/ansible3/bin/activate
pip install ansible
git clone https://github.com/jcardarelli/install-nodejs.git $HOME/ansible/roles/install-nodejs
cd $HOME/ansible/roles/install-nodejs
ANSIBLE_CONFIG=~/ansible/ansible.cfg ansible-playbook example-playbook.yml --limit localhost --ask-become-pass
```

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
git clone https://github.com/jcardarelli/install-nodejs.git $HOME/ansible/roles/install-nodejs
```

#### To install on localhost using example-playbook.yml
```
# Assuming your ansible working directory is $HOME/ansible
cd $HOME/ansible/roles/install-nodejs
ANSIBLE_CONFIG=~/ansible/ansible.cfg ansible-playbook example-playbook.yml --limit localhost --ask-become-pass
```

#### To install on a remote host
```
# Assuming your ansible working directory is $HOME/ansible
cd $HOME/ansible/roles/install-nodejs

# Copy blank playbook to a new playbook, and add in the values for host/hostgroup and the location of your ansible virtualenv directory
cp example-playbook-blank.yml $HOME/my-playbook.yml

# Assuming that ansible knows where to find your ansible.cfg file
ansible-playbook $HOME/my-playbook.yml --ask-become-pass
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

## Example `ansible-playbook` run

```console
you@your_computer:~/ansible/roles/install-nodejs$ ANSIBLE_CONFIG=~/ansible/ansible.cfg ansible-playbook example-playbook.yml --limit localhost --ask-become-pass
[DEPRECATION WARNING]: DEFAULT_MODULE_LANG option, Modules are coded to set their own locale if needed for screenscraping . This feature will be removed in version 2.9. Deprecation warnings can be disabled by setting 
deprecation_warnings=False in ansible.cfg.
BECOME password:

PLAY [all] ************************************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [install-nodejs : Install prerequisite packages, and update apt cache] *******************************************************************************************************************************************************************
[WARNING]: Could not find aptitude. Using apt-get instead

ok: [localhost]

TASK [install-nodejs : Install playbook prerequisite packages] ********************************************************************************************************************************************************************************
ok: [localhost]

TASK [install-nodejs : Find latest nodejs version from Github API] ****************************************************************************************************************************************************************************
ok: [localhost]

TASK [install-nodejs : Set variable with latest nodejs version] *******************************************************************************************************************************************************************************
ok: [localhost]

TASK [install-nodejs : Set variables for latest nodejs major version] *************************************************************************************************************************************************************************
ok: [localhost]

TASK [install-nodejs : Set other variables] ***************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [install-nodejs : Get latest nodejs major version] ***************************************************************************************************************************************************************************************
ok: [localhost] => {
      "nodejs_latest_major_version": "12"
}

TASK [install-nodejs : Get distribution release from ansible_facts variable] ******************************************************************************************************************************************************************
ok: [localhost] => {
      "msg": "stretch"
}

TASK [install-nodejs : Add nodesource GPG key with apt-key] ***********************************************************************************************************************************************************************************
ok: [localhost]

TASK [install-nodejs : Create apt sources list file for the nodesource repo] ******************************************************************************************************************************************************************
ok: [localhost]

TASK [install-nodejs : Install nodejs package, and update apt cache] **************************************************************************************************************************************************************************
ok: [localhost]

TASK [install-nodejs : Check that node and npm binaries are in /usr/bin] **********************************************************************************************************************************************************************
ok: [localhost] => (item=/usr/bin/node)
ok: [localhost] => (item=/usr/bin/npm)

PLAY RECAP ************************************************************************************************************************************************************************************************************************************
localhost                  : ok=13   changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

you@your_computer:~/ansible/roles/install-nodejs$
```

## License

BSD

## Author Information

https://github.com/jcardarelli/
