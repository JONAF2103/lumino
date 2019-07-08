# Get your own RIF Lumino node up and running on Ubuntu

## Prerequisites

1. Access to a synched RSK node. You can do this in a variety of ways:
	1. Run your own node on TestNet or MainNet, see [https://github.com/rsksmart/rskj/wiki/Install-RskJ-and-join-the-RSK-Orchid-Mainnet-Beta](https://github.com/rsksmart/rskj/wiki/Install-RskJ-and-join-the-RSK-Orchid-Mainnet-Beta)
	2. Compile and run a RSK node locally, see [https://github.com/rsksmart/rskj/wiki/Compile-and-run-a-RSK-node-locally](https://github.com/rsksmart/rskj/wiki/Compile-and-run-a-RSK-node-locally)
2. An RSK account with an RBTC balance NOT lower than 0.001 RBTC
3. Ubuntu 18.04+

## Install required libraries/software

### Install Python 3.7

Update your packages and install pre-requisites:

```
sudo apt update
sudo apt install software-properties-common
```

Add deadsnakes PPA to your sources list:

```
sudo add-apt-repository ppa:deadsnakes/ppa
```

Once the repository is enabled install Python 3.7:

```
sudo apt install python3.7
```


### Install Python 3.7-dev

If you didn't update your local APT repository:

```
sudo apt update
```

To install python 3.7-dev run the following command:

```
sudo apt-get install libpq-dev python3.7-dev
```

### Install PIP


If you didn't update your local APT repository:

```
sudo apt update
```

Install pip3:

```
sudo apt-get install python3-pip
```

### Install virtualenv

If you didn't update your local APT repository:

```
sudo apt update
```

Install virtualenv:

```
sudo apt-get install virtualenv
```



## Build RIF Lumino from code

1. Get the code from [https://github.com/rsksmart/lumino/releases/tag/0.0.1](https://github.com/rsksmart/lumino/releases/tag/0.0.1)
2. Uncompress the downloaded file
2. Go to the path you uncompressed the code in the previous step (lets call this path `$RIF_LUMINO_PATH`)
3. Create python virtual env for RIF Lumino (this needs to be performed only once) and execute the following command:

```
virtualenv -p <PATH_TO_PYTHON3.6> clientEnv
```

**Note:**
Replace `<PATH_TO_PYTHON3.6>` with the path where Python3.6 is installed in your system. In the case of Ubuntu OS, this is usually `/usr/bin/python3.6`

4. Activate python virtual env, by executing the following command:

```
source clientEnv/bin/activate
```

5. Check if the Python version is correct inside the virtual environment by running:

```
python --version
```

This command should output version 3.6.x

6. Install RIF Lumino requirements. Inside the virtual environment run the following command (this could take a few minutes):

```
pip install -c constraints.txt --upgrade -r requirements-dev.txt
```

7. Run Lumino setup with the following command:

```
python setup.py develop
```

##Start your RIF Lumino Node

1. Go to `$RIF_LUMINO_PATH`
2. If you haven't execute it before, run: source ``clientEnv/bin/activate``
3. Run the following command:

```
lumino
	 --rnsdomain=$RNS_DOMAIN_OF_YOUR_NODE_ADDRESS
	 --keystore-path $KEYSTORE_PATH
	 --network-id 31
	 --eth-rpc-endpoint $RSK_NODE_URL
	 --environment-type development
	 --tokennetwork-registry-contract-address=0x59ec7ced1e1ee2e4ccc74f197fb680d8f9426b96
	 --secret-registry-contract-address=0x4dea623ae7c5cb1f4af9b46721d9a72d93c42be9
	 --endpoint-registry-contract-address=0x7d1e6f17baa2744b5213b697ae4c1d287bb10df0
	 --no-sync-check
	 --api-address=127.0.0.1:5001

```

The following list describes each field:

| FIELD                                  | DESCRIPTION                                                                                                                |
|----------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| keystore-path                          | The path to your keystore                                                                                                  |
| eth-rpc-endpoint                       | URL of your RSK node (http://URL:PORT)                                                                                     |
| tokennetwork-registry-contract-address | Address for the token registry contract deployed (view contracts table for the contract address of testnet and mainnet)    |
| secret-registry-contract-address       | Address for the secret registry contract deployed (view contracts table for the contract address of testnet and mainnet)   |
| endpoint-registry-contract-address     | Address for the endpoint registry contract deployed (view contracts table for the contract address of testnet and mainnet) |


4. After you run the “lumino” command you will be presented with the following confirmation message:

```
Welcome to RIF Lumino Payments Protocol, Version 0.1

This is an Alpha version of experimental open source software released under the MIT license.
By using the RIF Lumino Payments Protocol (the “Software”), you acknowledge that this is a 
test version of the Software and assume the risk that the Software may contain errors and/or 
bugs. RIF Labs Limited (“RIF Labs”) makes no guarantees or representations whatsoever, 
including as to the suitability or use of the Software for any purpose or regarding its 
compliance with any applicable laws or regulations. By using the Software, you acknowledge 
that you have read this disclosure agreement, understand its contents, and assume all risks 
related to the use of of the software; further, by answering yes below and accepting the terms 
of this Agreement, you release and discharge RIF Labs, its officers, employees, or affiliates 
from, waive any claims you might have against RIF Labs, its officers, employees, or affiliates 
in connection with, and agree not to sue RIF Labs or any of its officers, employees, or 
affiliates for any direct or indirect liability arising from the use of this Software. 
----------------------------------------------------------------------
Privacy Warning:
By using the RIF Lumino Payments Protocol, you acknowledge that your RSK address, channels, 
channel deposits settlements, and the RSK address of your channel counterparty will be stored 
on the RSK blockchain—that is, on servers of RSK node operators—and therefore will be publicly 
available. The parties running nodes on the RIF Lumino network may also download and store 
this same or related information or data, and information or data stored on Lumino nodes and 
network channels will be publicly visible, including on a RIF Lumino block explorer. By using 
the Software and by answering yes below, you acknowledge that information or data stored on 
the Lumino network is extremely difficult to alter, remove, or delete; you further acknowledge 
that information or data related to individual tokens transfers will be made available via the 
Lumino Payments Protocol to the recipient intermediating nodes of a specific transfer as well 
as to the Lumino server operators. 
----------------------------------------------------------------------
Have you read and understood and do you accept the RIF Lumino Disclosure Agreement and Privacy 
Warning? [y/N]

press Y followed by Enter.

```

5. After you accepted you will be asked to select the account you want to use. Select the account and enter your passphrase to continue.


### Contract addresses table for each environment

| Contract                                | TestNet                                    | MainNet                                    |
|-----------------------------------------|--------------------------------------------|--------------------------------------------|
| Token Registry Contract | 0xa494fc762181ff78fe4cbb75d8609ccff1e63c1b | 0x59ec7ced1e1ee2e4ccc74f197fb680d8f9426b96 |
| Secret Registry Contract       | 0xfd17d36ef2b3c5e71aba059b3fc361644206213b | 0x4dea623ae7c5cb1f4af9b46721d9a72d93c42be9 |
| Endpoint Registry Contract     | 0xb048af6c0fbfbf1c0c01ea9a302987011153dbb8 | 0x7d1e6f17baa2744b5213b697ae4c1d287bb10df0 |

## Additional Help

### Install Python 3.6

(source: [http://ubuntuhandbook.org/index.php/2017/07/install-python-3-6-1-in-ubuntu-16-04-lts/](http://ubuntuhandbook.org/index.php/2017/07/install-python-3-6-1-in-ubuntu-16-04-lts/))

Add a new repository to you apt:

```
sudo add-apt-repository ppa:jonathonf/python-3.6
```

Update your local APT repository:

```
sudo apt-get update
```

Install Python 3.6:

```
sudo apt-get install python3.6
```

### Install Python 3.6-dev

To install python 3.6-dev run the following command:

```
sudo apt-get install libpq-dev python3.6-dev
```

### Install PIP


If you didn't update your local APT repository:

```
sudo apt update
```

Install pip3:

```
sudo apt-get install python3-pip
```

### Install virtualenv

If you didn't update your local APT repository:

```
sudo apt update
```

Install virtualenv:

```
sudo apt-get install virtualenv
```

