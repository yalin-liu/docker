COMP S381F Lab 11 

# Container-based Virtualization Using Docker

This tutorial demonstrates how to use Docker for running our Node.js apps. To do that, we have following lab tasks:

1. Docker Engine Installation
2. Get Started Using Docker Container
3. Multi-container Deployment


## 1. Docker Engine Installation

To make use of Docker container, we first need to install a Docker Engine on your computer systems. After that, Docker Desktop is provided to help us build, share, and run containers easily. In this tutorial, you will learn how to install Docker engine in Ubuntu.

*References:*
```
https://docs.docker.com/engine/install/
https://docs.docker.com/engine/install/ubuntu/
https://juejin.cn/post/6936010142475354148
```

### (a) Open your Ubuntu system

*Notes: To install Docker Engine, you need the 64-bit version of one of these Ubuntu versions. *

Open your Ubuntu system, and start a terminal. Type the following commands to uninstall old versions of Docker.

```
sudo apt-get remove docker docker-engine docker.io containerd runc
```

It’s OK if apt-get reports that none of these packages are installed.

### (b) Install using the repository

Update the apt package index and install packages to allow apt to use a repository over HTTPS:
```
sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```
Add Docker’s official GPG key:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add –
```
Check the GPG key:
```
sudo apt-key fingerprint 0EBFCD88
```
If the GPG key is added successfully, you will see the following:
```
pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
```
Add Docker’s official repository source:
```
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
Update the apt package and install the latest docker:

```
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### (c) Runnning and Testing

Type the following commands to your Ubuntu terminal:
```
sudo docker run hello-world
```
If you run the test successfully, you will see the following:
```
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.
...


```

Check the running Docker container:
```
docker ps -a
```

Remove the running Docker container and check the results.
```
docker rm -f a3d165377e2c
docker ps -a
```
*Replace `a3d165377e2c` by your Docker container ID.*

## 2. Get Started Using Docker Container

*Preparations:* 

- Download a Docker sample folder from github 

```
https://github.com/yalin-liu/docker.git
```
- Register at Docker Hub and obtain your Docker User ID (your-docker-id).

```
https://hub.docker.com/
```
By default, your docker-hub user name is your-docker-id. E.g., `ylliustudy` is my docker-hub user name and also my-docker-id.

### (a) Access the folder `comps381f`

This folder demonstrates how you run an express.js server, which requires an older version of Node (version 4), using container virtualization.

- Study all files, including `server.js`, `package.json`, and `Dockerfile`.

- Use `npm` to run server.js. Make a note of the version of Node being used.

### (b) Build a container image

- Create your Docker container
```
docker build -t "your-docker-id/oldnodejs" .
```
*Replace `your-docker-id` by your Docker user name.*

- Check your container image.
```
docker images
```

- Run your container

- Verify your container is running.
```
docker ps -a
```
### (c) Testing your app that runs on the docker container

- Open localhost:8099 in your Web broswer.

- Think about that? Which version of Node is being used now?

### (d) Push to Docker Hub

- Share your container image by uploading it to Docker Hub

```
docker login
docker push your-docker-id/oldnodejs
```
*Replace `your-docker-id` by your Docker user name.*

- Verify your uploading by checking `https://hub.docker.com/`.

- Remove the running Docker container and check the results. 


## 3. Multi-container Deployment

This lab task demonstrates how to deploy a multi-container app written using Express.js, Passport.js and MongoDB. Two containers are used to deploy this app. The first container bundles everything needed to run the app (which listens for HTTP requests at port 8099). The second container runs a MongoDB server used by the app running in the first container.

*Preparations:* 

- Access the sample folder `booking` in your downloaded `docker` folder.

### (a) Install `docker-compose`

Docker Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.

- Type the commands to install `docker-compose`
```
sudo apt install docker-compose
```
- Check your installation by typing 
```
docker-compose version
```

### (b) Modifications of `server.js`

- Add your mongourl.
- Replace the values of facebookAuth.clientID and facebookAuth.clientSecret in server.js with a valid Facebook App ID and App Secret.

### (c) Build and run two docker container images (booking_app and mongo)

- Run the following command
```
docker-compose up -d
```
- Check the running Docker container
```
docker ps -a
```
- Run the app by opening localhost:8099 in your web browser.

- Shutdhown the containers when you're done.
```
docker-compose down
```
- Remove the running Docker container and check the results. 
