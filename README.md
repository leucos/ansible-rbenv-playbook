Ruby/Rbenv with Ansible
=======================

This playbok demonstrates (ab)using roles to install several ruby
versions via rbenv.

# "Quick" start

    export ANSIBLE_HOST_KEY_CHECKING=false
    vagrant up
    until ping -c1 192.168.33.10 > /dev/null && ping -c1 192.168.33.11 >/dev/null; do sleep 1; done
    ansible-playbook -i hosts ruby.yml
    for i in 0 1; do echo -n ruby$i:" "; vagrant ssh ruby$i -c 'rbenv version'; done

# Vagrant

A Vagrantfile is provided for testing purposes. It will create two VMs,
and provision them with ansible.

    vagrant up

If you encounter this error :

    fatal: [ruby1] => {'msg': "FAILED: (25, 'Inappropriate ioctl for device')", 'failed': True}

get a newer vagrant version (1.3.5+) or issue :

    export ANSIBLE_HOST_KEY_CHECKING=false

before redoing a `vagrant up`.

Warm up machines network :

    until ping -c1 192.168.33.10 > /dev/null && ping -c1 192.168.33.11 >/dev/null; do
      sleep 1
    done

# The playbook

    ansible-playbook -i hosts ruby.yml -sku vagrant

will make your computer fans scream and cores smoke. Eventually, it will
install MRI 1.9.3-p448 and 2.0.0-p247 on both hosts with 2.0.0-p247
being the default Ruby on ruby0, and 1.9.3-p448 on ruby1.

You can check what happened with :

    for i in 0 1; do echo -n ruby$i:" "; vagrant ssh ruby$i -c 'rbenv version'; done

# Misc

Thanks to Ansible's Google Groups fellows for their help on this, and
especially Jerome Wagner for the role prereq trick.
Hack away, send PRs !

