# How to set up a 3 node Docker Swarm

## Installing Docker 
When we are setting up docker swarm on our 3 instances. One instance will be configured to be the master and the other 2 instances will be the workers.

### For all 3 instances do the following:
SSH into the instance:

```ssh -i <keypair.pem> ubuntu@<publicdnsname>```

Add the GPG key for the docker repository:

```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -```

Add the repository. You can choose to add the very latest. i.e. a release candidate or you can choose to add the latest stable version.

* For stable version:
  
  ```sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"```
* For latest version:
  
  ```sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) test"```

Update the package database:

```sudo apt-get update```

Make sure you are installing from the docker repo and not the ubuntu repo:

```apt-cache policy docker-ce```

Finally install docker:

```sudo apt-get install -y docker-ce```

OPTIONAL STEP to check the service is running:

```sudo systemctl status docker```

Add docker to current user so that you do not need sudo:

```sudo usermod -aG docker ${USER}```

### Configuring Docker Swarm (Master)
Pick any 1 of the EC2 instances and SSH into it.

```docker swarm init```

Copy the response to a file or clipboard. Sometihng like the following:

```docker swarm join --token <token> <ipaddress:port>```

### Configuring Docker Swarm (Workers)
For the other 2 instances SSH into each one and paste the text you copied from the master:

```docker swarm join --token <token> <ipaddress:port>```

### To test create a service (nexus in this test)
```docker service create --name=nexus3 --mode=global -p 80:8081 sonatype/nexus3:latest```

```docker service ls```

```curl <ipaddress>```