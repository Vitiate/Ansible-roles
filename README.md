SSHNG for Ansible
=================

A role for deploying and configuring SSH Public Keys from a GIT repository to a host

Can deploy all keys to the root user or deploy each username.pub file to a specific user.

Allows for easy configuration for both sudo and root user installations.


Supports
--------

Supported targets:

- RHEL 5+


Usage
-----

roles:
  -  { role: ../../rolesv2/security/sshng, SSHNG_ROOT: "yes", tags: ['sshng'] }

The SSHNG_ROOT variable controls the functionality of the installation:

SSHNG_ROOT: "yes" - Will apply all public keys to the root user.

SSHNG_ROOT: "no"  - Or not defined will create a new user for every public key located.

Configuration
-----

The defaults file sshng/defaults/main.yml contains the temporary file locations and the location of the git repository:

	git_repo: ssh://cs0-master/srv/git/pubkeys

	pubfile: /tmp/ssh_{{ inventory_hostname }}_pub_keys
	hostfile: /tmp/ssh_{{ inventory_hostname }}_host_keys
	temp_git: /tmp/ansible_ssh

GIT repository layout
-----

SSHNG expects to find files with the naming convention of username.pub files by this naming convention in the base directory will be applied to every host. 

Host Specific Keys / Users can be created in a subdirectory that mactches the inventory name of the host.


Still to do
-----------

- Add enforcing flag to the role, this will allow you to force remove keys that do not match the local repository.

- Use the enforcing flag to delete users that do not match the repository.


Changelog
---------

### 0.1

Initial version.