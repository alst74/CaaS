# Container as a Service with Vagrant

This repo will have playbooks for simple setup of different lab environments
Requirements:
- Vagrant
- Virtualbox
- ansible

You will get a docker swarm (docker-ee engine) and an easy way for installing UCP and/or DTR.

Todo:
- [x] Setup simple swarm mode with managers and workers
- [ ] Add license file in ucp/playbook.yml
- [ ] Some exercises to get UCP and DTR up and running

At the momemnt, it will bring up one manager/controller and 2 workers and it will be based on CentOS. Maybe more dists later on if needed/requested.
Pre steps:
1. Open https://store.docker.com/editions/enterprise/docker-ee-server-centos
2. Click on "Start 1 Month Trial" (tip: you can renew your trial after the expiration)
3. Download the license and copy the URL to your docker-ee repo

## Initial setup

```
git clone git@github.com:rjes/CaaS.git
```
Create the needed variable file:
```
cd CaaS
mkdir -p group_vars/all
echo 'docker_url: "YOUR DOCKER-EE URL"' > group_vars/all/main.yml
echo 'public_key: "YOUR SSH PUBLIC KEY"' >> group_vars/all/main.yml
``` 
Start and provision the virtual machines:
```
vagrant up
```
### UCP
```
ansible-playbook -i hosts ucp/playbook.yml
```
### DTR
```
ansible-playbook -i hosts dtr/playbook.yml
```

### Various command
To ssh to the controller node:
```
vagrant ssh controller1
```
or:
```
ssh -i /path/to/your/private_key vagrant@192.168.11.21 (or .51/.52 for workers)
```
sudo is password less

