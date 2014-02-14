Ruby/Rbenv with Ansible
=======================

This playbok demonstrates (ab)using roles to install several ruby
versions via rbenv.

## Pre-requisites

* [Vagrant 1.3.5+](https://docs.vagrantup.com/v2/)
* [Virtualbox](https://www.virtualbox.org/)
* [Ansible 1.4+](https://ansible.com)

## "Quick" start

```bash
vagrant up
ansible-playbook -i hosts ruby.yml
ansible all -i hosts -m command -a 'bash -lc "rbenv versions"' -u vagrant -c ssh
```

## Vagrant

A Vagrantfile is provided for testing purposes. It will create two VMs,
and provision them with ansible.

```bash
vagrant up
```

If you encounter this error :

```
fatal: [ruby1] => {'msg': "FAILED: (25, 'Inappropriate ioctl for device')", 'failed': True}
```

get a newer vagrant version (1.3.5+) or issue :

```bash
export ANSIBLE_HOST_KEY_CHECKING=false
```

before redoing a `vagrant up`.

## The playbook

```bash
ansible-playbook -i hosts ruby.yml
```

will make your computer fans scream and cores smoke. Eventually, it will
install MRI 2.1.0 and 2.0.0-p353 on both hosts with 2.0.0-p353
being the default Ruby on ruby0, and 2.1.0 on ruby1.

You can check what happened with :

```bash
ansible all -i hosts -m command -a 'bash -lc "rbenv versions"' -u vagrant -c ssh
```

## Thanks

Thanks to Ansible's Google Groups fellows for their help on this, and
especially Jerome Wagner for the role prereq trick.
Hack away, send PRs !

