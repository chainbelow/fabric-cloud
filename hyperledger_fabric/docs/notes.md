# Hyperledger Fabric 1.3
These notes are very crude. Please do not comment or ask questions on these.

## Compose New version 0.20
### Destroy old docker
```
docker kill $(docker ps -q)
docker rm $(docker ps -aq)
docker rmi $(docker images dev-* -q)
docker rm $(docker ps -a -q)
docker rmi $(docker images -q)
```

### Install Hyperledger Composer
```
npm install -g composer-rest-server@0.20
npm install -g composer-cli@0.20
npm install -g generator-hyperledger-composer@0.20
```

### Install Hyperledger Fabric 1.2 or 1.3+ 
```
mkdir fabric-dev-servers && cd fabric-dev-servers

curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.tar.gz
tar -xvf fabric-dev-servers.tar.gz

export FABRIC_VERSION=hlfv12
./downloadFabric.sh

./startFabric.sh
./createPeerAdminCard.sh
```

### Start a new project
```
yo hyperledger-composer:businessnetwork
* [ create a network called health-plan ]
cd health-plan
composer archive create -t dir -n .
composer network install --card PeerAdmin@hlfv1 --archiveFile health-plan@0.0.1.bna
composer network start --networkName health-plan --networkVersion 0.0.1 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file health-plan.card
composer card import --file health-plan.card
composer network ping --card admin@health-plan
composer-rest-server
* admin@health-plan
```

```
To restart the REST server using the same options, issue the following command:
   composer-rest-server -c admin@health-plan -n never -u true
```

## Start from Scratch (Docker or no docker)

```
# -- ubuntu
sudo apt-get -y install libssl-dev
```

```
# - macos
brew unlink openssl && brew link openssl --force
brew install openssl
export PATH="/usr/local/opt/openssl/bin:$PATH"' >> ~/.bash_profile
```

```
# - headers
export LDFLAGS="-L/usr/local/opt/openssl/lib"
export CPPFLAGS="-I/usr/local/opt/openssl/include"

brew install softhsm

# - install
curl -O https://dist.opendnssec.org/source/softhsm-2.0.0.tar.gz
tar -xvf softhsm-2.0.0.tar.gz
cd softhsm-2.0.0
./configure --disable-non-paged-memory --disable-gost
make
sudo make install
```

```
sudo mkdir -p /var/lib/softhsm/tokens
sudo chmod 777 /var/lib/softhsm/tokens
softhsm2-util --init-token --slot 0 --label "ForComposer" --so-pin 1234 --pin 98765432
```

