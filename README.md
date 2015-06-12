<!--

---
lang: american
---
-->

[![Build Status](https://travis-ci.org/cw-ansible/cw.vagrant-box.svg?branch=master)](https://travis-ci.org/cw-ansible/cw.vagrant-box)
[![Tweet this](http://img.shields.io/badge/Tweet-it00aced.svg)](https://twitter.com/intent/tweet?tw_p=tweetbutton&via=renard_0&url=https%3A%2F%2Fgithub.com%2Fcw-ansible%2Fcw.vagrant-box&text=Create%20environment%20to%20build%20a%20%23Vagrant%20base%20box%20with%20%23Ansible.)
[![Follow me on twitter](http://img.shields.io/badge/Twitter-Follow-00aced.svg)](https://twitter.com/intent/follow?region=follow_link&screen_name=renard_0&tw_p=followbutton)


# Vagrant-Box

Create environment for a vagrant base box.


## Usage

Include `cw.vagrant-box` role to your playbook.

If you install a new machine using the *chroot* method with the
[system-install](https://github.com/cw-ansible/system-install) role, please
note that you need to first reboot the machine before running
`cw.vagrant-box`.

## Description

This module will install `vagrant` user as described in the
[Creating a base box](http://docs.vagrantup.com/v2/boxes/base.html)
manifest:

- user `vagrant` with password `vagrant` using the insecure ssh key pair.
- `sudo` is passwordless for `vagrant`.
- root password is *not* changed since it is not mandatory.
- `sshd` uses option `UseDNS no`.

In addition, this roles also install `VirtualBoxAddition` modules to be
integrated with Virtual Box.

### Rant

Since *DKMS* is not able to build pure-binary modules, and we don't want to
waste space with a compilier tool-chain we need to compile *VirtualBox*
additions, and install kernel modules inside the module load path manually.

A bug (and a fix-patch) has been
[submitted](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=554843]), but
no one seems to be interested in it (and providing full binary packages).

## Configuration

Nothing is done here.

## How to

Once the role has been executed on the `VBOX_NAME` machine, you need to
create the base box from `vagrant`:
	
	vagrant package --base VBOX_NAME --output /path/to/BASE_BOX_NAME.box

Then you can initialize `vagrant` from a work directory:

	vagrant init MY_NEW_BOX /path/to/BASE_BOX_NAME.box

Finaly the box is available for any usage:

	vagrant up
	vagrant ssh

## Links

- [Vagrant Documentation](http://docs.vagrantup.com/v2/)
- [Vagrant installation packages](http://www.vagrantup.com/downloads)
- [VirtualBox](https://www.virtualbox.org/)
- [VirtualBox installation packages](https://www.virtualbox.org/wiki/Downloads)

## Copyright

Author: Sébastien Gross `<seb•ɑƬ•chezwam•ɖɵʈ•org>` [@renard_0](https://twitter.com/renard_0)

License: WTFPL, grab your copy here: http://www.wtfpl.net
