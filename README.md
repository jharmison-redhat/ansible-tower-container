# Ansible Tower in a container - demo

## Don't push this image anywhere - it has your RHSM creds and potentially Tower license in it.

---

This demo is to spin up Ansible Tower in a single container on your local machine (or a remote one, if you modify the inventory) using Podman as the container runtime and Ansible as the configuration mechanism.

### Use

1. Preinstall `ansible` of version 2.9 or higher
1. Preinstall `podman` and ensure you can run rootless containers on your OS of choice
1. Copy `host_vars/podman_host.example.yml` to `host_vars/podman_host.yml` and update it with the information relevant for you (using the comments there as a guide)
1. \[OPTIONAL\] Edit `hosts.yml` to update which host you want to be doing the podman work on
1. \[OPTIONAL\] If you want to use your own TLS certificates instead of self-signing them, you can place them in the project root as `tower.cert` and `tower.key` after enabling the variables. They have been .gitignored.
1. `ansible-galaxy collection install -r requirements.yml` to install the podman Ansible Collection content
1. `ansible-playbook playbooks/build.yml` to build (if new version of Ansible)
1. `ansible-playbook playbooks/run.yml` to build (if new version of Ansible) and run
1. `ansible-playbook playbooks/stop.yml` to stop Tower, leaving it ready to start again
1. `ansible-playbook playbooks/destroy.yml` to stop and remove Tower

So, for instance, you could prepare with `build`, begin your demo with `run`, and then bring the environment down non-destructively with `stop` to use another day.

### What works

- You can build and run Ansible Tower in Fedora 31+ with rootless podman with SELinux enforcing in a grand total of about 7 minutes.
- It runs as a single container and can be persistent across starts/stops/rms/creates.
- You can provide your own TLS cert/key.

### What doesn't work yet (but will)

- Specifying a license to use with the new Manifest mechanism
- Specifying python packages for automatic inclusion in the default virtualenv
- Specifying an inventory and preloading it
- Specifying a set of projects to sync and presyncing them

### What won't work

- PgSQL persistence if you remove the built container image
  - This means that containers spawned from the image should be fine, but every individual image requires its own persistence directory if you're trying to start more than one or something.

### What might work

- RHEL 8 host?

### Specs

The following are some times that I measured at the time of this writing:

| Task                                    | Time    |
|-----------------------------------------|--------:|
| Starting and running Tower from scratch |   7m 2s |
| Stopping a Tower container              |     12s |
| Starting a Tower container again        |     14s |
| Removing everything                     |     18s |

The final image is about 1.9GB right now. I can get that down to 1.7GB at best, but it takes longer and isn't really worth it. DO NOT PUSH THIS IMAGE ANYWHERE :)
