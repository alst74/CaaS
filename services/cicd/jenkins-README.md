## Jenkins CICD
### Todo

[ ] Prebake Jenkins with needed configuration files

[ ] Rewrite this file, not 5 min before bedtime.

[ ] Setup webhook and all things with API instead of manual actions.



There are some manual steps that needs to be done before we are ready to go.

1. If you dont already have your client bundle:
```
export UCP_FQDN=192.168.11.21
AUTHTOKEN=$(curl -sk -d '{"username":"admin","password":"admin123"}' https://${UCP_FQDN}/auth/login | cut -d\" -f4)
curl -k -H "Authorization: Bearer $AUTHTOKEN" -s https://${UCP_FQDN}/api/clientbundle -o bundle.zip && unzip bundle.zip
export DOCKER_TLS_VERIFY=1
export COMPOSE_TLS_VERSION=TLSv1_2
export DOCKER_CERT_PATH=$PWD
export DOCKER_HOST=tcp://192.168.11.21:443
```

2. Create the stack
```
docker stack deploy -c jenkins.yml
```

3. Setup Jenkins according to the configuration files in /Jenkins directory
(Later, I can maybe prebake all the config files into a custom jenkins image)

4. Setup the webhook in gitea towards Jenkins
Create an admin user by register a new user in gitea, the first user is the admin user.<br>
Create your repo and client on settings and webhook, add new webhook: <br>
`http://admin:admin123@192.168.11.51:8080/generic-webhook-trigger/invoke?token=build`

5. Setup DTR to send webhooks:<br>
Create repo, click on webhooks and enter the URI:<br>
`http://admin:admin123@192.168.11.51:8080/generic-webhook-trigger/invoke?token=deploy`

6. Create a git repo and add a `Dockerfile` and a `docker-compose.yml` files:<br>
(Just a single oneline Dockerfile is enough now)<br>
```
FROM jwilder/whoami
```

And your docker-compose.yml

```
version: '3'
services:
  mywhoami:
    image: dtr.docker.lab/admin/mywhoami:latest
    ports:
      - 8000
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
```

7. Push and everything should work unless I have done some bad writing ;)
