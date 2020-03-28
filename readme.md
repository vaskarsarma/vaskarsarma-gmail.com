- To install nginx server with replica
docker service create --name nginx --replicas=5 nginx

- To view docker service(cluster) list
docker service ps nginx

- To get list of containers
docker ps -a

- To get all docker images
docker images

- to get list of master and worker nodes
docker node ls

- To setup Master docker swarm
On Master Node >> docker swarm init
Response as below 
Swarm initialized: current node (vxmcp3nl8lzctg10d74thszxn) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-3pj09nbzh0h1hzsxhsdoj22vv5l6d055yqoze0r2v240idhak8-0xwgccb2kbliomnsr6gbe46gv 172.31.33.207:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions. 

On Worker Node >> run the command as shown below
[root@ip-172-31-33-7 ~]# docker swarm join --token SWMTKN-1-3pj09nbzh0h1hzsxhsdoj22vv5l6d055yqoze0r2v240idhak8-0xwgccb2kbliomnsr6gbe46gv 172.31.33.207:2377
This node joined a swarm as a worker.

Once above is done, please run this command on Master Node
docker node ls
should display the list of mapped Master and Worker Nodes. Response would be like as below:
[root@ip-172-31-33-207 ~]# docker node ls
ID                            HOSTNAME                        STATUS              AVAILABILITY        MANAGER STATUS      ENGINE VERSION
1a1gs3z9aakmx319ybbp5qiep     ip-172-31-33-7.ec2.internal     Ready               Active                                  18.09.9-ce
vxmcp3nl8lzctg10d74thszxn *   ip-172-31-33-207.ec2.internal   Ready               Active              Leader              18.09.9-ce
xdjjwxpl9gh3znsj2b8yyqnin     ip-172-31-40-226.ec2.internal   Down                Active                                  18.09.9-ce
[root@ip-172-31-33-207 ~]#


--------------------------------------------------------------------------------------------------------

To build a node app
>> docker build -t vaskarsarma/myapp .

To view images
>> docker images
λ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
vaskarsarma/myapp   latest              c225edbe5fcf        17 minutes ago      918MB

To run a docker images - will create a docker container
>> docker run -p 49160:3000 -d vaskarsarma/myapp

To view docker container
>>  docker ps

# Get container ID
$ docker ps

# Print app output
$ docker logs <container id>

# Example
Running on http://localhost:3000

# Enter the container
$ docker exec -it <container id> /bin/bash

To test a docker images
curl -i localhost:49160 

----------------------------------------------------------------------------------

> docker images
> docker run -ti <imagename> bash >> will start a container for the image and open the container terminal
> docker commit <container ID> <new-image-tag> >> to commit any changes within docker container for the image and this will create a new image
> docker images >> will display the new image name
> docker run -ti <new image name> bash >> will start a new container and open the container terminal in bash
> docker run <new image name > >> will start a new container
> docker ps -a >> will display all the container
> docker ps >> will display on the runnning container
> docker ps -l >> will display last accessed container

---------------------------------------------------------------------------------------
> docker run --rm -ti vaskarsarma/myapp sleep 5 >> use --rm command to delete a container after sleep for 5s
> docker run -ti vaskarsarma/myapp bash -c "sleep 3; echo All Done" >> will start the container after sleep for 3s
e.g. :
D:\Softwares\cmder_mini
λ docker run -ti vaskarsarma/myapp bash -c "sleep 3; echo all done"
all done

D:\Softwares\cmder_mini ( Will delete the container)
λ docker run --rm -ti vaskarsarma/myapp bash -c "sleep 3; echo all done"
all done

> docker ps -a >> will show list of new container if any

-----------------------------------------------------------------------------------------
Dettached and attached a container

> D:\Softwares\cmder_mini
λ docker run -d -ti vaskarsarma/myapp bash
ab6cd1b00c04f14e38825ebffb7c88eaa79c95acf95429358eb16c0436e5c682

D:\Softwares\cmder_mini
λ docker attach ab6cd1b00c04
root@ab6cd1b00c04:/usr/src/app# ls
Dockerfile  index.js  node_modules  package-lock.json  package.json
root@ab6cd1b00c04:/usr/src/app# read escape sequence

>> to exit the container process press >> ctrl + p and ctrl + q

Even if i exist the process >> cotainer will keeep on running , will not stop.
> docker ps >> will display the running container

------------------------------------------------------------------------------------------

docker exec
>> is used to start a another process within an existing container

1st Terminal >>

D:\Softwares\cmder_mini
λ docker run -ti  vaskarsarma/myapp bash
root@e6aa8d69cc25:/usr/src/app# ls
Dockerfile  index.js  node_modules  package-lock.json  package.json

2nd Terminal >>

D:\Softwares\cmder_mini
λ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
e6aa8d69cc25        vaskarsarma/myapp   "docker-entrypoint.s…"   25 seconds ago      Up 22 seconds       3000/tcp            dazzling_shockley

D:\Softwares\cmder_mini
λ docker exec -ti  e6aa8d69cc25 bash
root@e6aa8d69cc25:/usr/src/app# ls
Dockerfile  index.js  node_modules  package-lock.json  package.json
root@e6aa8d69cc25:/usr/src/app# touch vaskar
root@e6aa8d69cc25:/usr/src/app# ls
Dockerfile  index.js  node_modules  package-lock.json  package.json  vaskar

1st Terminal >>

root@e6aa8d69cc25:/usr/src/app# ls
Dockerfile  index.js  node_modules  package-lock.json  package.json  vaskar

-------------------------------------------------------------------------------------------







