# Jenkins at home

```
# Run Docker daemon without sudo (requires logout)
sudo groupadd docker
sudo usermod -aGdocker wes

docker build -t jenkins-data -f Dockerfile-data .
docker build -t jenkins .

# Run 
docker run --name=jenkins-data jenkins-data
docker run -p 8080:8080 -p 50000:50000 --name=jenkins-master --volumes-from=jenkins-data -d -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker jenkins 

# Get initial admin password
docker exec jenkins-master cat /var/jenkins_home/secrets/initialAdminPassword
```

Go to Jenkins at localhost:8080/

## Bash shell into container
docker exec -it jenkins-master bash


### References
[DZone - Get Started with Jenkins 2.0 with Docker](https://dzone.com/articles/get-started-with-jenkins-20-with-docker)
