# Docker commands
### build docker image from a dockerfile
you may need to create an image with different components. You write these in the dockerfile and run form cmd as follow
`docker build -t imagenameyoulike -f Dockerfile . --no-cache`

https://medium.com/@yvescallaert/docker-intro-building-a-python-3-image-62031d0b7e39

https://medium.com/faun/how-to-build-a-docker-container-from-scratch-docker-basics-a-must-know-395cba82897b

### get an image from cloud
`docker pull imagename`

### run and image
`docker run -it imagename:version`

e.g docker run -t ubuntu:latest


### to get out of runing container

when the image is running, it is container

`press ctrl + p and ctrl + q`

### check runing container list
`docker ps -a`

you will see runing container list, copy the id by selecting with mouse and ctrl + check

### get back into running container
`docker attach continer_id`

you can add applications and modules in the running container. But once stop all new applications
installed will be lost. Therefore you need to freeze the running container as a new image
### create new image with newly installed application
`docker commit container_id new_imagename:version`

Note: the new image is somehow child image of previous one and thus you may need to create the stanalone image from scratch using DockerFile.

### removing images
`docker images -a` to see the image ids, copy the image id to remove in next step

`docker rmi -f image_id image_id`

for more info on "How To Remove Docker Containers, Images, Volumes, and Networks": https://linuxize.com/post/how-to-remove-docker-images-containers-volumes-and-networks/

### how to run jupyterlab
`docker run -it -d -p 8888:8888 image_name:tag`

example: docker run -it -d -p 8888:8888 datascience-python3:version3

(if you dont see any messages after the command, the container is running quitely in the background. You can check it with `docker ps -a` and copy the id to get into it with `docker attch id` command. When inside the container, run below cmd..)

`python3 -m jupyterlab --allow-root  --ip=0.0.0.0 --port=8888`

you will see a few lines of infor with toke information like `http://127.0.0.1:8888/?token=f95ae233b84ca517ddc049c57b8219a4589ce117f8d0e5ee` copy it and paste into your browser to start Jupyterlab



