# Explanation

- it isn't included with docker.
```CMD
docker --version
docker-compose --vresion
```
- First, create `docker-compose.yml` file.
```docker-compose.yml
version: "3"
services:
	node-app: 
		container_name: express-node-app-container
		build: .
		volumes:
			- ./src:/app/src:ro
		ports:
			- "4000:4000"				
```
- Instead of writing a long command to build and run:
```CMD
docker run --name express-node-app-container -v $(pwd)/src:/app/src:ro -p 4000:4000 express-node-app
```
- We can use docker-compose command:
```CMD
docker-compose up
```
- Or
```CMD
docker-compose up -d
```
- The image name will be the root folder name  the service name: `my-express-app_node-app`.
- To close container:
```CMD
docker-compose down
```

# Sources
- [Video 9 - Docker Practical Course in Arabic](https://youtu.be/k1Yg4UsrHqs?si=c646Ij89CXHU2brZ)
- [Docker Compose](https://docs.docker.com/compose/)