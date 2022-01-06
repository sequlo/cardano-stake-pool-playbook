# cardano-stake-pool
This repository contains Ansible scripts for provisioning a Cardano stake pool.

## Requirements
Make sure Ansible is installed on the Ansible control node. Ansible scripts are tested on hosts with Ubuntu 20.04, but should theorically work with any Debian-based Linux distro.

Each managed node's `ansible_user` should have passwordless `sudo` and the public key of the provisioning user installed.

## Define inventory file
Edit `hosts.yml`, which by default defines a Cardano stake pool with one relay node, which also caries the role of monitoring server, one core (block producing) node and the SPO's host, in this example `localhost`. It is also possible to define multiple relays and/or designate a seperate host for monitoring. It might be a good idea to have multiple inventory files, each one targeting a different network e.g. `mainnet-hosts.yml`, `testnet-hosts.yml`, etc.

## How to Run
Configure an inventory file e.g. `my-testnet-pool-inventory.yml`, with something like:

```yaml
---
all:
  vars:
    node_network: testnet
  hosts:
    operator:
      ansible_host: localhost
      ansible_connection: local
    core:
      ansible_host: csp-core-node
      ansible_user: ada
      node_host: csp-core-node
      node_port: 6000
    monitor:
      ansible_host: csp-relay-node-01
      ansible_user: ada
  children:
    relays:
      hosts:
        relay-01:
          ansible_host: csp-relay-node-01
          node_host: 111.222.333.444
      vars:
        ansible_user: ada
        node_port: 6000
```

Now run:

```bash
$ ansible-playbook -i my-testnet-pool-inventory.yml pool.yml
```

The core component installed on almost every host is of course `cardano-node` and is managed by a `systemd` service installed by the `cardano-node-service` role. By default the node services are not enabled and started on provisioning. This will give the SPO the opportunity to verify and possibly alter configuration.

Check out the `README.md` files in the [role folders](./roles) for more information.
