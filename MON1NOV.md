# MON 1 NOV

## Kubernetes Session 2 10:00-02:30
## 1Nov - Wed - Session 2
## Check this image from blackboard for reference: https://i.imgur.com/YDL5kxD.jpg

- root vs rootless container (always make rootless)
unsecure vs secure
from root vs from home

- docker file = container file (container file is for podman)
Dockerfile has some instruction like FROM, ADD, COPY, RUN, CMD, ENTRYPOINT (ALL CAPS)

- explanation
FROM  docker.io/library/ubunut:latest (Write entire registry url, good practice instead of ubuntu:latest)
(for instll) RUN yum install httpd -y (httpd is apache) ( we can run multiple commands) 
COPY code.tar /var/www/html
ADD code.tar /var/www/html (will directly untar, same as copy)
CMD apache -D foreground
every FROM, COPY, etc. line is a different layer ( line 1 = layer 2) sequence of each layer is very important
we can create the container in docker file from the normal container user but we define a user inside the container
docker file has some level of 
podman build -t himanshu-httpd:v1 . (we add the image here)
first we got the os and then installed apache image, 

- ONE CONTAINER SHOULD HAVE ONE APPLICATION - GOOD PRACTICE - But you can try for understanding - Otherwise its wrong

- pv 
podman run -itd --name httpd -P 9-9-"9-
- lets sau o have /var/log as my log location and i wnt to use it as the log in my container as well
changes in persistent volume in the 
- se linux if "." is at the end if ls -ld under the first column of permission then volume 
- podman run -itd --name httpd -- -v/home/yash/logs -P 8080: httpd:latest 
- podman logs <container>
- podman inspect allows you to see everythig=ng about how a container was made including the first podman run command
- node is just thevirtua machine on wich the container is running
- create an image of ubuntu - might be done without dockerfile

