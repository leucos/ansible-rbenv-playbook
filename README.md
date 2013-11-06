Ruby/Rbenv with Ansible
=======================

This playbok demonstrates (ab)using roles to install several ruby
versions via rbenv, thanks to JErome Wagner role dependency trick.
`vagrant up`

# Vagrant

A Vagrantfile is provided for testing purposes :

`vagrant up`

If you encounter this error :

```
fatal: [ruby1] => {'msg': "FAILED: (25, 'Inappropriate ioctl for
device')", 'failed': True}
```
get a newer vagrant version or issue :

`export ANSIBLE_HOST_KEY_CHECKING=false`

before redoing a `vagrant up`

# Testing the playbook

`ansible-playbook -i hosts ruby.yml`

will install MRI 1.9.3-p448 and 2.0.0-p247 on both hosts.
