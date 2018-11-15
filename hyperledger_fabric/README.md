# Hyperledger Fabric
This is a fork from forked from yeasy/docker-compose-files. This project provides several useful Docker-Compose script to help quickly bootup a Hyperledger Fabric network, and do simple testing with deploy, invoke and query transactions.

Hyperledger Fabric all releases from v0.6 to latest v1.3 are supported.

# Installation
## Operating System
* http://releases.ubuntu.com/16.04/
## Prerequisites
* curl -O https://hyperledger.github.io/composer/v0.19/prereqs-ubuntu.sh
* chmod u+x prereqs-ubuntu.sh
* ./prereqs-ubuntu.sh


## Supported Fabric Releases

Fabric Release | Description
--- | ---
[Fabric Latest](latest/) | latest fabric code, unstable.
[Fabric v1.3.0](v1.3.0/) | stable fabric 1.3.0 release.
[Fabric v1.2.0](v1.2.0/) | stable fabric 1.2.0 release.
[Fabric v1.1.0](v1.1.0/) | stable fabric 1.1.0 release.
[Fabric v1.0.6](v1.0.6/) | fabric v1.0.6 release.
[Fabric v1.0.5](v1.0.5/) | fabric v1.0.5 release.
[Fabric v1.0.2](v1.0.2/) | fabric v1.0.2 release.
[Fabric v1.0.0](v1.0.0/) | fabric v1.0.0 release.
[Fabric v0.6.0](v0.6.0/) | fabric v0.6.0 release (too old, not recommend to use).


## Getting Started

### Start here

```bash
RELEASE=v1.3.0
$ cd ${RELEASE}; make setup test
```

### Pick a fabric version

Change into the sub folder of specific version and setup

```bash
$ cd ${RELEASE} # select a fabric version
$ make setup download # Install docker/compose, and pull required images
```

### Quick Test

The following command will run the entire process (start a fabric network, create channel, test chaincode and stop it.) pass-through.

```bash
$ make test  # Test with default fabric solo mode
```

### Test with more modes

```bash
$ HLF_MODE=solo make test # Bootup a fabric network with solo mode
$ HLF_MODE=couchdb make test # Enable couchdb support, web UI is at `http://localhost:5984/_utils`
$ HLF_MODE=event make test  # Enable eventhub listener
$ HLF_MODE=kafka make test # Bootup a fabric network with kafka mode
$ HLF_MODE=be make test  # Start a blockchain-explorer to view network info
```

## Detailed Steps

See [detailed steps](docs/steps.md)

## Acknowledgement

* [Hyperledger Fabric](https://github.com/hyperledger/fabric/) project.
