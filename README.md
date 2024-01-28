<h1> Containers_Docker </h1>
To deploy containers quickly with root ssh connetion


<h2> REF Shanika Wickramasinghe:  </h2>
https://www.cherryservers.com/blog/ssh-into-docker-container

<h3> Create the image registry </h3>
Use the Dockerfile and launch this command in the file repository
docker build -t davidimage .

<h3> Test fonctionality of the registry image </h3>
docker run -d -p 2222:22 --name test davidimage
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'  test
Log / passwd    :    root / root


<h2> REF Scritp shell Xavki </h2>
https://xavki.blog/dockeransible-comment-se-creer-un-mini-datacenter-de-test-sans-vm-parc-de-conteneurs/

<h3> Use the container.sh script with controle of your ssh rsa key and the name of the image registry </h3>
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