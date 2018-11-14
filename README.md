# Jenkins 2 With Docker
Learning :: How to install/config the Continuous Integration Server with Jenkins on Docker 

* Jenkins master 
* Jenkins data to keep all configuration such as plugins and jobs of Jenkins

## Build:
```
docker build -t jenkins-data -f data/Dockerfile .
docker build -t jenkins2 -f master/Dockerfile .
```

## Run:
```
docker run --name=jenkins-data jenkins-data
docker run -p 8080:8080 -p 50000:50000 --name=jenkins --volumes-from=jenkins-data -d jenkins2
```
## Start Jenkins servers recursively with Docker:
```
docker run -p 8080:8080 -p 50000:50000 -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker --name=jenkins --volumes-from=jenkins-data -d jenkins2
```

## Get Jenkins Password:
```
docker exec jenkins2 cat /var/jenkins_home/secrets/initialAdminPassword
```

## Set Up SSH Keys:
```
ssh-keygen -t rsa
ssh-copy-id jenkins@172.16.0.213
ssh 172.16.0.213
```