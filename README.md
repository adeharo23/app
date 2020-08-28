# app 

docker network create jenkins
docker volume create jenkins-docker-certs

docker container run --name jenkins-docker --rm --detach --privileged --network jenkins --network-alias docker --env DOCKER_TLS_CERTDIR=/certs --volume jenkins-docker-certs:/certs/client --volume jenkins-data:/var/jenkins_home --volume /mnt/c/Users/asier.deharo/Desktop/JenkinsHome:/home docker:dind

docker container run --name jenkins-tutorial --rm --detach --network jenkins --env DOCKER_HOST=tcp://docker:2376 --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 --volume jenkins-data:/var/jenkins_home --volume jenkins-docker-certs:/certs/client:ro --volume /mnt/c/Users/asier.deharo/Desktop/JenkinsHome:/home --publish 8080:8080 --publish 50000:50000 jenkinsci/blueocean

docker container ls

docker exec id cat /var/jenkins_home/secrets/initialAdminPassword

https://www.jenkins.io/doc/tutorials/build-a-node-js-and-react-app-with-npm/
