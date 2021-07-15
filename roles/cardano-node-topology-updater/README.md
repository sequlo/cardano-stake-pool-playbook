# cardano-node-topology-updater role
Installs `cardano-node-topology-updater`, which for now wraps [Guild Operators' `topologyUpdater.sh` script](https://cardano-community.github.io/guild-operators/Scripts/topologyupdater/), for updating the topology configuration of a locally running `cardano-node`.

This role also configures a cronjob running this tool every hour in order to update the topology configuration. The way peers are discovered at the moment is quite a spartan approach for such suffisticated software, heance slightly disappointing, and postponed to be implemented in a future releases of `cardano-node`.

Note that `cardano-node` has to be manually restarted for the new topology configuration to take effect. This tool's primary objective is just updating the topology configuration.