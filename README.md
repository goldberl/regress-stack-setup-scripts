## Launching OpenStack via [regress-stack](https://github.com/canonical/regress-stack) on Multipass VMs for Testing
### Regress Stack

Regress Stack is an Ubuntu OpenStack package configurator created by Canonical.
It is designed to simplify setting up a single-node OpenStack environment for testing purposes.

With Regress Stack, you can install and configure OpenStack services and run basic smoke tests to verify functionality.

---
### About this Repo
This repository contains cloud-init configurations for provisioning a regress-stack development and testing environment on Ubuntu 22.04 (Jammy) and Ubuntu 24.04 (Noble).

It includes automation for:

- Installing required system packages
- Setting up optional Ubuntu Cloud Archive (UCA) repositories
- Installing development tools (git, uv, micro)
- Cloning and configuring regress-stack
- Running OpenStack package installation
- Executing regress-stack setup and validation tests

---
### Horizon Support
This fork of regress-stack includes Horizon support, which is not currently available in the upstream regress-stack repository.

Once provisioning is complete, Horizon can be accessed at:
```
http://<VM-IP-ADDRESS>/horizon
```
---
### Usage

Launch a Multipass VM with cloud-init:

```
multipass launch <ubuntu-release> --name regress-stack --cpus 8 --memory 16G --disk 50G --cloud-init <script.yaml>
```

Access the VM
```
multipass shell regress-stack
```

Follow the cloud-init script live
```
sudo tail -f /var/log/cloud-init-output.log
```

Once the script is done, follow the instructions at end to complete the setup.
