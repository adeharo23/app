# app 

docker network create jenkins
docker volume create jenkins-docker-certs

//Aqui se levantará el deploy en el puerto 3000(adaptar al puerto de nuestra app)
docker container run --name jenkins-docker --rm --detach \
  --privileged --network jenkins --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins-data:/var/jenkins_home \
  --volume "$HOME":/home \
  --publish 3000:3000 docker:dind
 
 //Jenkins (accedo mediante http://localhost:8080/)
docker container run --name jenkins-tutorial --rm --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  --volume "$HOME":/home --publish 8080:8080 jenkinsci/blueocean

docker container ls

//Obtener password por defecto para loguearse a jenkins
docker exec id cat /var/jenkins_home/secrets/initialAdminPassword

//Info proceso de CI/CD en Jenkins
https://www.jenkins.io/doc/tutorials/build-a-node-js-and-react-app-with-npm/
