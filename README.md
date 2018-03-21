# Container as a Service with Vagrant

This repo will have playbooks for simple setup of different lab environments
Requirements:
- Vagrant
- Virtualbox
- ansible


At the momemnt, it will bring up one manager/controller and 2 workers

## Initial setup
Download your docker licence file and put it under $HOME
```
git clone git@github.com:rjes/CaaS.git
```
Review the files so everything matches your environment, you need to add your license file and the URI to your docker-ee repo:
```
cp ~/docker_subscription.lic .
echo 'docker_url: "YOUR DOCKER-EE URL"' > group_vars/all/secrets.yml
echo 'public_key: "YOUR SSH PUBLIC KEY"' >> group_vars/all/main.yml
```
Start and provision the virtual machines:
```
vagrant up
```
### UCP (docker enterprise dashboard)
```
ansible-playbook -i hosts ucp/playbook.yml
```

### Vagrant commands
To ssh to the controller node:
```
vagrant ssh controller1
```
