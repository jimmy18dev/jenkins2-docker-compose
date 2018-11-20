# Jenkins 2 With Docker
Jenkins for Continuous Integration (CI) and the other uses people have found for it as a task/batch file runner and cron substitute. Install and config the Continuous Integration Server with Jenkins on Docker

* Jenkins master 
* Jenkins data to keep all configuration such as plugins and jobs of Jenkins
* Mount the host machine's Docker socket in the container.

## Docker Compose:
```
docker-compose up -d --build && clear && docker-compose ps
```

## Build:
```
docker build -t jenkins-data -f data/Dockerfile .
docker build -t jenkins2 -f master/Dockerfile .
```

## Docker Run:
```
docker run --name=jenkins-data jenkins-data
docker run -p 9000:8080 -p 50000:50000 --name=jenkins2 --volumes-from=jenkins-data -d jenkins2
```

## Start Jenkins servers recursively with Docker:
```
docker run -p 9000:8080 -p 50000:50000 -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker --name=jenkins2 --volumes-from=jenkins-data -d jenkins2
```

Port 8080 exposes the web interface and port 50000 gives you access to a remote Java (JIRA) API.

## Get Jenkins First Password:
```
docker exec jenkins2 cat /var/jenkins_home/secrets/initialAdminPassword
```

## Set Up SSH Keys:
```
ssh-keygen -t rsa
ssh-copy-id jenkins@172.16.0.213
ssh 172.16.0.213
```
