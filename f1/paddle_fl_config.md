
export FL_MASTER_SERVICE_HOST=127.0.0.1
export FL_MASTER_SERVICE_PORT_FL_MASTER=8000
export FL_SERVER_SERVICE_HOST=127.0.0.1
export FL_SERVER_SERVICE_PORT_FL_SERVER=8001
export FL_SCHEDULER_SERVICE_HOST=127.0.0.1
export FL_SCHEDULER_SERVICE_PORT_FL_SCHEDULER=8002
export TRAINER0_SERVICE_HOST=127.0.0.1
export TRAINER0_SERVICE_PORT_TRAINER0=8003
export TRAINER1_SERVICE_HOST=127.0.0.1
export TRAINER1_SERVICE_PORT_TRAINER1=8004
alias python=/home/gjh/pad36_pip/bin/python

sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get install python3.6
sudo apt-get install python3.6-venv
python3.6 -m venv pad36
source pad36/bin/activate
alias python=pad36/bin/python
curl https://bootstrap.pypa.io/get-pip.py | python -


HLF_VERSION=2.2.1
docker pull hyperledger/fabric-peer:${HLF_VERSION}
docker pull hyperledger/fabric-orderer:${HLF_VERSION}
docker pull hyperledger/fabric-ca:${HLF_VERSION}
docker pull hyperledger/fabric-ccenv:${HLF_VERSION}
docker-compose -f test/fixtures/docker-compose-2orgs-4peers-tls.yaml up

