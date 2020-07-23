# Ansible Tower in a container - demo

---

This demo is to spin up Ansible Tower in containers on your local machine (or a remote one, if you modify the inventory) using Podman as the container runtime and Ansible Engine as the configuration mechanism.

To use:

1. Preinstall `ansible` of version 2.9 or higher
1. Preinstall `podman` and ensure you can run rootless containers on your OS of choice
1. Copy `host_vars/podman_host.example.yml` to `host_vars/podman_host.yml` and update it with the information relevant for you (using the comments there as a guide)
1. \[OPTIONAL\] Edit `hosts.yml` to update which host you want to be doing the podman work on
1. \[OPTIONAL\] If you have an Ansible Tower license `.json` file (e.g. from [the workshop license link](https://www.ansible.com/workshop-license)), you can place it at the project root as `tower_license.json`
1. `ansible-galaxy collection install -r requirements.yml` to install the podman Ansible Collection content
1. `ansible-playbook playbooks/build.yml` to install
1. `ansible-playbook playbooks/destroy.yml` to uninstall
