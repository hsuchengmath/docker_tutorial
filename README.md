# docker tutorial

1. Install docker on Ubuntu-18.04
   => [https://phoenixnap.com/kb/how-to-install-docker-on-ubuntu-18-04]

2. show all image
```
docker image ls
```

3. delete image
```
docker image rm [imageName]
```

4. pull hello-world image from dockerhub
```
docker image pull hello-world
```

5. run hello-world by image
```
docker container run hello-world
```

6. run image and simultaniously interactive with a tag, where -it = 'interactive'.
```
docker container run -it ubuntu bash
```

6. show container running now
```
docker container ls
```

7. kill container
```
docker container kill [containerId]
```







