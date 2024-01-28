# Containers_Docker
To deploy containers quickly with root ssh connetion


# REF Shanika Wickramasinghe:
https://www.cherryservers.com/blog/ssh-into-docker-container

# Create the image registry
Use the Dockerfile and launch this command in the file repository
docker build -t davidimage .

# Test fonctionality of the registry image
docker run -d -p 2222:22 --name test davidimage
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'  test
Log / passwd    :    root / root


# REF Scritp shell Xavki
https://xavki.blog/dockeransible-comment-se-creer-un-mini-datacenter-de-test-sans-vm-parc-de-conteneurs/

# Use the container.sh script with controle of your ssh rsa key and the name of the image registry
You have to controle that the  id_rsa key exist and that his name is yhe same than in the container.sh file
On the file, this is his line :
docker cp ${HOME}/.ssh/id_rsa.pub ${USERNAME}-vmparc${i}:${HOME}/.ssh/authorized_keys
The command to create the id_rsa is :
ssh-keygen
This key is on the host at this location : /root/.ssh/

You have to controle that the name of the image registry create just above is the same name than in the container.sh file
Mine is "davidimage"

On the file, this is his line :
docker run -tid -v /sys/fs/cgroup:/sys/fs/cgroup:ro --name ${USERNAME}-vmparc${i} davidimage
