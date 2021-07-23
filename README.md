# cardano-stake-pool
This repository contains Ansible scripts for provisioning a Cardano stake pool.

## Install Ansible
The machine running these Ansible scripts should have Ansible installed.

## Define inventory file
Edit `hosts.yml`, which by default defines a Cardano stake pool with one relay node, which also caries the role of monitoring server, one core (block producing) node and the SPO's host, in this example `localhost`. It is also possible to define multiple relays and/or designate a seperate host for monitoring. It might be a good idea to have multiple inventory files, each one targeting a different network e.g. `mainnet-hosts.yml`, `testnet-hosts.yml`, etc.

## Prepare hosts
Ansible scripts are tested on hosts with Ubuntu 20.04, but should theorically work with any Debian-based Linux distro; hence there is a dependency on the APT-packaging system.

Make that each host's `ansible_user` has passwordless `sudo`, for some Ansible tasks require becoming root:

```bash
$ sudo visudo
```

Append the following:

```
<USERNAME> ALL=(ALL) NOPASSWD: ALL
```

Use `ssh-copy-id` to install the public key on managed nodes.

## How to Run
With an inventory file called `hosts.yml` playbooks can be run in tandem by issueing the `pool.yml` playbook like so:

```bash
$ ansible-playbook -i hosts.yml pool.yml
```
To target specific actors just use their specific playbook instead, e.g. to only provision the relay nodes do:

```bash
$ ansible-playbook -i hosts.yml pool-relay-nodes.yml
```

The core component installed on almost every host is of course `cardano-node` and is managed by a `systemd` service installed by the `cardano-node-service` role. By default the node services are not enabled and started on provisioning. This will give the SPO the oppertunity to verify and possibly alter configuration.

Check out the `README.md` files in the [role folders](./roles) for more information.
