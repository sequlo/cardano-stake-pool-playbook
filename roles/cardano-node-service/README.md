# cardano-node-service role
Installs `cardano-node` as a `systemd` service.

```
/etc/systemd/system
  /cardano-node.service # `systemd` service definition for `cardano-node`
/usr/local/bin
  /cardano-node-service # bash script for managing the service
/usr/local/lib/sequlo/cardano-node
  /start-node # bash script sourcing the node configuration used for starting a `cardano-node`
/usr/local/etc/sequlo/cardano-node
  /network # network configuration (config.json, topology.json, *-genesis.json) grouped in folders by network
  /node.conf # node configuration declares which network configuration to use and other `cardano-node` parameters
/var/local/sequlo/cardano-node
  /db # the node's database grouped in folders by network
```

# Usage
This role does not enable and start the service giving the SPO the opertunity to tweek configuration before starting `cardano-node`. This role also does not overwrite existing node configuration and network configuration.

When the configuration is verified the service should be enabled and started like so:

```bash
$ cardano-node-service enable
$ cardano-node-service start
```

Verify the node is running correctly by issuing the following commands:

```bash
$ cardano-node-service status
$ cardano-node-service log
```

Other commands can be discovered by reading the usage information when `cardano-node-service` is ran without arguments.