# Docker commands
### build docker image from a dockerfile
you may need to create an image with different components. You write these in the dockerfile and run form cmd as follow
`docker build -t imagenameyoulike -f Dockerfile . --no-cache`

https://medium.com/@yvescallaert/docker-intro-building-a-python-3-image-62031d0b7e39

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

### removing images
`docker images -a` to see the image ids, copy the image id to remove in next step

`docker rmi -f image_id image_id`

