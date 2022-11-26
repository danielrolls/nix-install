nix-install
=========

[![Galaxy](https://img.shields.io/badge/galaxy-danielrolls.nix-blue.svg?style=flat-square)](https://galaxy.ansible.com/danielrolls/nix/)


This is an Ansible role that installs the [nix](https://nixos.org/) package manager.
At the time of writing, all other roles I've seen that install nix, install a single user nix.
This role invokes the multi-user installation as recommended by the manual to ensure build isolation.
The role supports upgrading nix versions for which nix is uninstalled to allow the installer to work.
This role is also extremely simple and hence easy to adapt.


Requirements
------------

This should work with any Linux distribution that uses systemd.
It has been tested with Ubuntu.

Role Variables
--------------
nix_version -- The version of nix to download and install.
If unset this role will take the latest nix version it has been tested with.

installer_checksum -- A checksum for the installer binary.
You will need to change this if you change the nix version that is downloaded.
It's easiest to let this fail and fix the error since the error is clear and provides the new checksum value to copy in.

nix_commands -- Optional list of shell commands to run in an environment with nix and the running nix daemon.

flakes -- Set to enable nix flake commands.

config -- Optionally pass addition config to be added to the nix configuration file


Example Playbook
----------------

This example installs nix for all users on myhost
```
- hosts: myhost
  roles:
    - role: danielrolls.nix
```

This example also installs nix for all users on myhost and then installs and runs nix-info.
See the [NixOS homepage](https://nixos.org/) for examples of commands to run.
```
- hosts: myhost
  roles:
    - role: danielrolls.nix
      nix_commands:
      - "nix-shell -p nix-info --command nix-info" 
```

License
-------

MIT

Author Information
------------------

[Github Profile](https://github.com/danielrolls)
