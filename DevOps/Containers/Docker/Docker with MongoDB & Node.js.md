# Explanation

- To add a new service, we first need to search the [Docker Hub Website](https://hub.docker.com/) to see how to add it in the [[Docker Compose]].
```docker-compose.yml
version: "3"
services:
	node-app: 
		container_name: express-node-app-container
		build: .
		ports:
			- "4000:4000"
		env_file:
			- ./.env
	mongo:
	    image: mongo
	    restart: always
	    environment:
	      MONGO_INITDB_ROOT_USERNAME: root
	      MONGO_INITDB_ROOT_PASSWORD: example
```
- In node.js server:
```Node.js
const DB_USER = 'root';
const DB_PASSWORD = 'example';
const DB_PORT = 27017; // from PORTS when run (docker ps)
const URL = `mongodb://${DB_USER}:${DB_PASSWORD}@host:${DB_PORT}`;
mongoose.connect(URL);
```
- How to know IP address (host) of mongodb container?
```CMD
docker inspect my-express-app-mongo_1
```
- In `Networks` we can find `IPAddress`.
- Or in this way:
```CMD
docker network ls
docker network incpect my-express-app-default
```
- **Or just use service name as a host:**
```Node.js
const DB_HOST = 'mongo';
```
## Problem
- **Because the container is just an in-memory process, when using this method all the data and database we built are removed when the container is rebuilt. So, we need to install all the data on the hard drive.**

# Sources
- [Video 13 - Docker Practical Course in Arabic](https://youtu.be/XP98uQ_2JIQ?si=tDbqBIgEa5kP3MqU)
- [Docker Hub - Mongo](https://hub.docker.com/_/mongo)
