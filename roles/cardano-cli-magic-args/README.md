# cardano-cli-magic-args role
Installs `cardano-cli-magic-args` which, when run, simply echo's the 'magic' argument associated with a currently running `cardano-node-service` managed `cardano-node` instance.

# Usage
This tool comes in handy for SPO's running `cardano-cli` commands against a locally running `cardano-node`. Can be used like so:

```bash
$ cardano-cli query tip `cardano-cli-magic-args`
```