
# Explanation

- A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image.
- When we build Dockerfile the output is image.

  ```Dockerfile
 /** From baseimage **/
 FROM node:20 #install node.js with version 20 inside the container
 WORKDIR /app 
 COPY package.json . #copy new file and directories to the image's filesystem
 /*
 we can also do this: 
 COPY package.json ./app
 */
 RUN npm install #install dependency
 COPY . . #copy all files and dirs to the container
 EXPOSE 4000 #just for documination
 CMD ["npm", "start"]
 ```
 We can also write in this way, but it isn't efficient due docker cache:
 ```Dockerfile
 FROM node:20 
 WORKDIR /app 
 COPY . .
 RUN npm install
 EXPOSE 4000
 CMD ["npm", "start"]
```
- ![[container.png]]
- To build Dockerfile:
`express-node-app` is the name of image we created.
```CMD
docker build -t express-node-app .
```
- To view all our images:
```CMD
docker image ls
```
- To run container on terminal:
`express-node-app-container` is the name of container.
```CMD
docker run --name express-node-app-container express-node-app
```
- To run container outside terminal:
add `-d`
```CMD
docker run --name express-node-app-container -d express-node-app
```
- To view all containers running:
```CMD
docker ps
```
- To remove container:
`-f` is for force the system to stop if container is still running.
```CMD
docker rm express-node-app-container -f
```
- [Port Forwarding:](https://docs.docker.com/guides/docker-concepts/running-containers/publishing-ports/)
_Port forwarding_ is a crucial method for _Docker_ that allows you to expose _container_ ports to the outside world.
```CMD
docker run -d -p HOST_PORT:CONTAINER_PORT nginx
```
- `HOST_PORT`: The port number on your host machine where you want to receive traffic.
- `CONTAINER_PORT`: The port number within the container that's listening for connections.
So:
```CMD
docker run --name express-node-app-container -d -p 4000:4000 express-node-app
```

# Sources
- [Video 4 - Docker Practical Course in Arabic](https://youtu.be/og6jyK1U4rw?si=z11EIXj63jultIrp)
- [Port Forwarding - Publishing and exposing ports](https://docs.docker.com/guides/docker-concepts/running-containers/publishing-ports/)