# cardano-hd-wallet role
Installs `cardano-hd-wallet`, a shell script for working with Hierarchical Deterministic (HD) wallets.

# Usage
This tool is intended to be used by SPO's for managing the SPO's and owners' stake pool wallets. This tool expects a wallet phrase file (`wallet.phrase`) in the current working directory. If you need to work with a new wallet simply run:

```bash
$ cardano-hd-wallet init
```

This will generate a new `wallet.phrase` file for you in the current directory.

The tool exposes several commands for working with the wallet. Execute the tool without arguments to read about the available commands.
