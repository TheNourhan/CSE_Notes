# Explanation

- To solve this problem [[Docker with MongoDB & Node.js#Problem]] we will use [[Docker Volumes]].
- Where to Store Data? [Docker Hub - mongo ](https://hub.docker.com/_/mongo)
	- Create a data directory on the host system (outside the container) and [mount this to a directory visible from inside the container⁠](https://docs.docker.com/storage/bind-mounts/). This places the database files in a known location on the host system, and makes it easy for tools and applications on the host system to access the files. The downside is that the user needs to make sure that the directory exists, and that e.g. directory permissions and other security mechanisms on the host system are set up correctly.
	1. Create a data directory on a suitable volume on your host system, e.g. `/my/own/datadir`.
	2. Start your `mongo` container like this:
	    ```console
	    $ docker run --name some-mongo -v /my/own/datadir:/data/db -d mongo
	    ```
	- The `-v /my/own/datadir:/data/db` part of the command mounts the `/my/own/datadir` directory from the underlying host system as `/data/db` inside the container, where MongoDB by default will write its data files.
	- This image also defines a volume for `/data/configdb`[for use with `--configsvr` (see docs.mongodb.com for more details)⁠](https://docs.mongodb.com/v3.4/reference/program/mongod/#cmdoption-configsvr)
- Create volumes:
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
	    volumes:
		    - mongo-db:/data/db
	    environment:
	      MONGO_INITDB_ROOT_USERNAME: root
	      MONGO_INITDB_ROOT_PASSWORD: example

volumes:
	mongo-db:
```
- When stop the container, volumes are not stopping. We need to pass `-v` with command to remove all volumes of container. **BUT it's dangerous.**
```CMD
docker-compose -f docker-compose.yml -f docker-compose.dev.yml down -v
```
## Mongo-Express
- To use the UI when working with a Mongo database, we can use: Mongo-Express [Docker Hub - mongo ](https://hub.docker.com/_/mongo).
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
	    volumes:
		    - mongo-db:/data/db
	    environment:
	      MONGO_INITDB_ROOT_USERNAME: root
	      MONGO_INITDB_ROOT_PASSWORD: example

	mongo-express:
	    image: mongo-express
	    restart: always
	    ports:
	      - 8081:8081
	    environment:
	      ME_CONFIG_MONGODB_ADMINUSERNAME: root
	      ME_CONFIG_MONGODB_ADMINPASSWORD: example
	      ME_CONFIG_MONGODB_URL: mongodb://root:example@mongo:27017/
	      ME_CONFIG_BASICAUTH: false

volumes:
	mongo-db:
```

# Sources
- [Video 14 - Docker Practical Course in Arabic](https://youtu.be/dcrdobTJsLM?si=VFuXTnMeRso-Sgm7)
- [Docker Hub - Mongo](https://hub.docker.com/_/mongo)