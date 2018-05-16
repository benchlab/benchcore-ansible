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

ELK Stack is an Elastic stack (Elastic search, Logstash and Kibana) and this script uses Logz.io as the service provider for the ELK Stack. You can set up your nodes to log there automatically. Create an account and get your API key from the notes via [https://app.logz.io/#/dashboard/data-sources/Filebeat](https://app.logz.io/#/dashboard/data-sources/Filebeat).

**CENTOS INSTALL**
```
yum install systemd-devel
go get github.com/mheese/journalbeat
ansible-playbook -i inventory/digital_ocean.py -l benchchain-testnet logzio.yml -e LOGZIO_TOKEN=YOUR-LOGZ-TOKEN
```

**UBUNTU INSTALL**
```
apt-get install libsystemd-dev
go get github.com/mheese/journalbeat
ansible-playbook -i inventory/digital_ocean.py -l benchchain-testnet logzio.yml -e LOGZIO_TOKEN=YOUR-LOGZ-TOKEN
```

