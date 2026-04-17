## Launching OpenStack via [regress-stack](https://github.com/canonical/regress-stack) on Multipass VMs for Testing
### Regress Stack

Regress Stack is an Ubuntu OpenStack package configurator created by Canonical.
It is designed to simplify setting up a single-node OpenStack environment for testing purposes.

With Regress Stack, you can install and configure OpenStack services and run basic smoke tests to verify functionality.

---
### About this Repo
This repository contains cloud-init configurations for provisioning a regress-stack development and testing environment on Ubuntu 22.04 (Jammy) and Ubuntu 24.04 (Noble).

**It includes automation for:**

- Installing required system packages
- Setting up optional Ubuntu Cloud Archive (UCA) repositories
- Installing development tools (git, uv, micro)
- Cloning and configuring regress-stack
- Running OpenStack package installation
- Executing regress-stack setup and validation tests

**At the end of the script, some manual setup will need to be done.**

1. Source the auth creds
```
sudo cp /root/auth.rc ~ && sudo chown $(id -u):$(id -g) ~/auth.rc && source ~/auth.rc
```

2. Validate the openstack token
```
openstack token issue
```

3. Run the regress-stack playground
```
cd regress-stack && sudo uv run regress-stack playground
```

4. Get the user creds (and ousrce if you want to use those instead of auth creds)
```
sudo cp /root/user.rc ~/user.rc
```

5. Deploy a server
```
openstack server create --image ubuntu-<release> --flavor m1.small --network private-network test-server

```

---
### Horizon Support
The [fork of regress-stack that this script uses](https://github.com/goldberl/regress-stack/tree/add-horizon-support) includes Horizon support, which is not currently available in the upstream regress-stack repository.

**Once provisioning is complete, Horizon can be accessed at:**
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
