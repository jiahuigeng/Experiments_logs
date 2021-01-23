network.sh

根据 docker-compose-test-net 发起docker-compose 

cryptogen and ca are parallels:
services:
	orderer.example.com  based on fabric-orderer exec: orderer

	peer0.org1.example.com based on fabric-peer exec: peer node start
	peer0.org2.example.com

	cli based on fabric-tools  exec: bash



	ca_org1:  based on fabric-ca         exec: sh -c 'fabric-ca-server start -b admin:adminpw -d'
	ca_org2:  based on fabric-ca         exec: sh -c 'fabric-ca-server start -b admin:adminpw -d'

	ca_orderer: based on fabric-ca       exec: sh -c 'fabric-ca-server start -b admin:adminpw -d'


	create orgs:
	  	cryptogen generate --config=./organizations/cryptogen/crypto-config-org1.yaml --output="organizations"
    	cryptogen generate --config=./organizations/cryptogen/crypto-config-orderer.yaml --output="organizations"

	create consortium:
	 	configtxgen -profile TwoOrgsOrdererGenesis -channelID system-channel -outputBlock ./system-genesis-block/genesis.block


	ca create orgs:

  		fabric-ca-client enroll -u https://admin:adminpw@localhost:7054 --caname ca-org1 --tls.certfiles ${PWD}/organizations/fabric-ca/org1/tls-cert.pem

  	  	register peer0 msp
  	  	fabric-ca-client enroll -u https://peer0:peer0pw@localhost:7054 --caname ca-org1 -M ${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/msp --csr.hosts peer0.org1.example.com --tls.certfiles ${PWD}/organizations/fabric-ca/org1/tls-cert.pem

  	  	generate peer0-tls certificates
  	  	fabric-ca-client enroll -u https://peer0:peer0pw@localhost:7054 --caname ca-org1 -M ${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls --enrollment.profile tls --csr.hosts peer0.org1.example.com --csr.hosts localhost --tls.certfiles ${PWD}/organizations/fabric-ca/org1/tls-cert.pem

  	  	generate user msp
  	  	fabric-ca-client enroll -u https://user1:user1pw@localhost:7054 --caname ca-org1 -M ${PWD}/organizations/peerOrganizations/org1.example.com/users/User1@org1.example.com/msp --tls.certfiles ${PWD}/organizations/fabric-ca/org1/tls-cert.pem

  	  	generate org admin msp
  	  	abric-ca-client enroll -u https://org1admin:org1adminpw@localhost:7054 --caname ca-org1 -M ${PWD}/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp --tls.certfiles ${PWD}/organizations/fabric-ca/org1/tls-cert.pem

  		register peer:
  		fabric-ca-client register --caname ca-org1 --id.name peer0 --id.secret peer0pw --id.type peer --tls.certfiles ${PWD}/organizations/fabric-ca/org1/tls-cert.pem

  		register user:
  	  	fabric-ca-client register --caname ca-org1 --id.name user1 --id.secret user1pw --id.type client --tls.certfiles ${PWD}/organizations/fabric-ca/org1/tls-cert.pem

  	  	register org admin:
  	  	fabric-ca-client register --caname ca-org1 --id.name org1admin --id.secret org1adminpw --id.type admin --tls.certfiles ${PWD}/organizations/fabric-ca/org1/tls-cert.pem








TO READ:
	test-network/organizations/fabric-ca/