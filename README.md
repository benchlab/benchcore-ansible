<p align="center">
  <img src="https://github.com/benchlab/benchx-media/raw/master/bench-logo.png" width="100px" alt="Bench Logo"/>
</p> <br>

# Official Ansible Deploy Script For BenchCore
Official Ansible deploy script for BenchCore using DigitalOcean as the default provider.

## Prerequisites For Ansible-Based BenchCore Deployments 
- Install Ansible 2.0 or higher via [https://www.ansible.com](https://www.ansible.com) on a Linux VM or your local environment. Must be Linux or Mac OSX-based.
- Create a DigitalOcean API token via [https://cloud.digitalocean.com/settings/api/tokens](https://cloud.digitalocean.com/settings/api/tokens)
- Make Sure DigitalOcean API token has read/write capabilities
- Create SSH keys
- Install the Python `dopy` package for the Digital Ocean Python functions to work correctly.

## Deploying BenchCore With Ansible

The playbooks are located here [https://github.com/benchlab/benchcore-ansible/tree/master/](https://github.com/benchlab/benchcore-ansible/tree/master/)

```
### to configure the sentry node architecture.

ansible roles
export API="your-digital-ocean-token"
export KEY="$HOME/.ssh/id_rsa.pub"

# This deployer assumes that you have your rocketeer set up already.
# You can create the folder structure for the BenchCore nodes using `benchcore testnet`.
# For example: benchcore testnet --v 0 --n 4 --o build/
# Then copy your dawn.json and modify the config.toml as you see fit.

ansible-playbook -i inventory/digital_ocean.py -l benchchain-testnet install.yml
ansible-playbook -i inventory/digital_ocean.py -l benchchain-testnet config.yml -e BENCH=`pwd`/build/benchcore -e BCONFIG=`pwd`/build

```

### Using ELK Stack For Deploying Error and Event Logging 

ELK Stack is an Elastic stack (Elastic search, Logstash and Kibana) and this script uses Logz.io as the service provider for the ELK Stack. You can set up your nodes to log there automatically. Create an account and get your API key via [https://app.logz.io/#/dashboard/data-sources/Filebeat](https://app.logz.io/#/dashboard/data-sources/Filebeat).

**CENTOS INSTALL**
```
yum install systemd-devel
go get github.com/mheese/journalbeat
ansible-playbook -i inventory/digital_ocean.py -l benchchain-testnet elk.yml -e LOGZIO_TOKEN=YOUR-LOGZ-TOKEN
```

**UBUNTU INSTALL**
```
apt-get install libsystemd-dev
go get github.com/mheese/journalbeat
ansible-playbook -i inventory/digital_ocean.py -l benchchain-testnet elk.yml -e LOGZIO_TOKEN=YOUR-LOGZ-TOKEN
```

## VERSION 
1.0.3

## LICENSE 
BENCH LICENSE
For BenchChain-Terraform

Copyright (c) 2018 Bench Computer, Inc. <legal@benchx.io>

Permission to use, copy, modify, and distribute this blockchain-related
software or blockchain-based software for any purpose with or without 
fee is hereby granted, provided that the above copyright notice and this 
permission notice appear in all copies.

THE USAGE OF THIS BLOCKCHAIN-RELATED OR BLOCKCHAIN-BASED SOFTWARE WITH THE
PURPOSE OF CREATING ICOS OR "INITIAL COIN OFFERINGS", UNREGISTERED SECURITIES 
SPECIFICALLY IN THE UNITED STATES OR IN OTHER COUNTRIES THAT HAVE A LEGAL 
FRAMEWORK FOR SECURITIES, IS PROHIBITED. BENCH FOUNDATION, LLC RESERVES THE 
RIGHT TO TAKE LEGAL ACTION AGAINST ANY AND ALL COMPANIES OR INDIVIDUALS WHO
USE THIS BLOCKCHAIN-RELATED OR BLOCKCHAIN-BASED SOFTWARE FOR THE PURPOSE OF 
DISTRIBUTING CRYPTOCURRENCIES WHERE THOSE CRYPTOCURRENCIES AND THEIR METHOD
OF DISTRIBUTION ARE IN DIRECT VIOLATION OF UNITED STATES SECURITIES LAWS. 
IF A GOVERNMENT BODY TAKES ACTION AGAINST ANY USERS, DEVELOPERS, MARKETERS,
ORGANIZATIONS, FOUNDATIONS OR ANY PROFESSIONAL ENTITY WHO CHOOSES TO UTILIZE
THIS SOFTWARE FOR THE DISTRIBUTION OF ILLEGAL SECURITIES, BENCH COMPUTER INC.
WILL NOT BE HELD LIABLE FOR ANY ACTIONS TAKEN BY THE USERS, DEVELOPERS, MARKETERS,
ORGANIZATIONS, FOUNDATIONS OR ANY PROFESSIONAL ENTITIES WHO CHOOSE TO DO SO.

UNITED STATES SECURITIES VIOLATIONS SPECIFICALLY REFER TO ANY VIOLATIONS OF
SECTION 10(b) OF THE SECURITIES EXCHANGE ACT OF 1934 [15 U.S.C. § 78j(b)] AND
RULE 10b-5(b) PROMULGATED THEREUNDER [17 C.F.R. § 240.10b-5(b)], AND
SECTIONS 5(a), 5(c), and 17(a)(2) OF THE SECURITIES ACT OF 1933 [15 U.S.C.
§§ 77e(a), 77e(c), and 77q(a)(2)]; BY MAKING USE OF ANY MEANS OR INSTRUMENTS
OF TRANSPORTATION OR COMMUNICATION IN INTERSTATE COMMERCE OR OF THE MAILS TO
SELL THROUGH THE USE OR MEDIUM OF ANY WRITTEN CONTRACT, OFFERING DOCUMENT,
PROSPECTUS, WHITEPAPER, OR OTHERWISE, ANY SECURITY AS TO WHICH NO REGISTRATION
STATEMENT WAS IN EFFECT. OR FOR THE PURPOSE OF SALE OR DELIVERY AFTER SALE,
CARRYING OR CAUSING TO BE CARRIED THROUGH THE MAILS OR IN INTERSTATE COMMERCE,
BY MEANS OR INSTRUMENTS OF TRANSPORTATION OR COMMUNICATION IN INTERSTATE
COMMERCE OR OF THE MAILS TO OFFER TO SELL OR OFFER TO BUY THROUGH THE USE OR 
MEDIUM OF ANY WRITTEN CONTRACT, OFFERING DOCUMENT, PROSPECTUS, WHITEPAPER,
OR OTHERWISE, SECURITIES AS TO WHICH NO REGISTRATION STATEMENT HAS BEEN FILED.

OUTSIDE OF THESE LEGAL REQUIREMENTS, THIS SOFTWARE IS PROVIDED "AS IS" AND 
THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING 
ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL 
THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL 
DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, 
WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, 
ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
