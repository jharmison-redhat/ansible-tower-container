# Ansible Tower in a container - demo

---

This demo is to spin up Ansible Tower in a single container on your local machine (or a remote one, if you modify the inventory) using Podman as the container runtime and Ansible as the configuration mechanism.

To use:

1. Preinstall `ansible` of version 2.9 or higher
1. Preinstall `podman` and ensure you can run rootless containers on your OS of choice
1. Copy `host_vars/podman_host.example.yml` to `host_vars/podman_host.yml` and update it with the information relevant for you (using the comments there as a guide)
1. \[OPTIONAL\] Edit `hosts.yml` to update which host you want to be doing the podman work on
1. \[OPTIONAL\] If you have an Ansible Tower license `.json` file (e.g. from [the workshop license link](https://www.ansible.com/workshop-license)), you can place it at the project root as `tower_license.json` after enabling the variables. It has been .gitignored.
1. \[OPTIONAL\] If you want to use your own TLS certificates instead of self-signing them, you can place them in the project root as `tower.cert` and `tower.key` after enabling the variables. They have been .gitignored.
1. `ansible-galaxy collection install -r requirements.yml` to install the podman Ansible Collection content
1. `ansible-playbook playbooks/build.yml` to build (if new version of Ansible)
1. `ansible-playbook playbooks/run.yml` to build (if new version of Ansible) and run
1. `ansible-playbook playbooks/stop.yml` to stop Tower, leaving it ready to start again
1. `ansible-playbook playbooks/destroy.yml` to stop and remove Tower

So, for instance, you could prepare with `build`, begin your demo with `run`, and then bring the environment down non-destructively with `stop` to use another day.
