# cardano-stake-pool role
Installs `cardano-stake-pool`, a shell script for working with stake pools.

# Usage
This tool is intended to be used by SPO's in order to setup and manage a stake pool. The tool's working is kept as simple as possible to not overcomplicate things in the script's source code; hence keeping it maintainable. To discover the tools features simply run the it without passing any arguments or pass `-h` (also after every (sub)command). When things to not work out as expected you can trace the issue by enabling trace output by passing `-X` as first argument.

To create a new stake pool setup, create a new empty directory, and from inside that directory run:

```bash
$ cardano-stake-pool init
```

Initialization can be tweaked by passing certain arguments such as the number of pool owners and whether the SPO is actually one of the owners. See the usage printed by the tool for more information.

Now edit `pool.conf`, which contains the pool's configuration mostly making up the stake pool registration certificate.

The `spo` and `owner-*` folders contain the keys and addresses needed for pool registration, delegation, etc. Now you could of course replace the initialized keys and addresses with existing onces you got elsewhere. You could for example use `cardano-hd-wallet` to initialize wallets in the `owner-*` and `spo` folders and use it the derive the keys and addresses to overwrite the initialized ones.

Once you're sattisfied with the keys and addresses just make sure to fund the SPO's payment address, for it is used to pay transaction fees and for example the stake pool deposit on pool registration.

Metadata is not mandatory for registering a stake pool, but if you do have metadata, now is the time to publish it on the web and make sure it is matching the hash and url declared in `pool.conf`.

You can now issue a dry-run omitting transaction submition so you can check the registration procedure and files generated:

```bash
$ cardano-stake-pool -X register --dry-run
```

If everything checks out, just do:

```bash
$ cardano-stake-pool register
```

The core node has to be configure to run `cardano-node` for block producing. Suppose you have the user `ada` configuration for running `cardano-node` on your core node host, than you cold create a folder like:

```bash
$ sudo mkdir -p /usr/local/etc/sequlo/cardano-node/pool
$ sudo chown ada@ada /usr/local/etc/sequlo/cardano-node/pool
```

Export the operational certificate along with the KES and VRF signing keys to the core node with something like:

```bash
$ cardano-stake-pool export ada@csp-core-node/usr/local/etc/sequlo/cardano-node/pool
```

Edit `/usr/local/etc/sequlo/cardano-node/node.conf` like so:

```bash
NODE_SHELLEY_KES_KEY="$NODE_ETC_DIR/pool/kes.skey"
NODE_SHELLEY_VRF_KEY="$NODE_ETC_DIR/pool/vrf.skey"
NODE_SHELLEY_OPERATIONAL_CERTIFICATE="$NODE_ETC_DIR/pool/node-operational.cert"
```

Now issue:

```bash
$ cardano-node-service restart
```

When this tool is used in conjunction with `cardano-hd-wallet` all the basic functionality is provided to facilitate further stake pool operations such as withdrawing rewards, retiring the pool, renewing the operational certificate, etc. Check out usage information printed by the tools for more information.