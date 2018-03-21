# Container as a Service with Vagrant

This repo will have playbooks for simple setup of different lab environments
Requirements:
- Vagrant
- Virtualbox

## Initial setup
Download your docker licence file and put it under $HOME
```
git clone <this repo> CaaS
```
Review the files so everything matches your environment
```
cp ~/docker_subscription.lic .
vagrant up
```
### UCP (docker enterprise dashboard)
```
ansible-playbook -i hosts ucp/playbook.yml
```

