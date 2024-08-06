# Explanation

- If we have multiple environments like: `docker-compose.dev.yml`, `docker-compose.prod.yml`, etc..
```CMD
docker-compose -f docker-compose.dev.yml up -d
docker-compose -f docker-compose.dev.yml down
```
- We can constant a [[Docker Compose]] file, and split the rest of the environment into a separate file with its own instructions, without repetition.
- In `docker-compose.yml`:
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
```
- In `docker-compose.dev.yml`:
```docker-compose.yml
version: "3"
services:
	node-app: 
		volumes:
			- ./src:/app/src:ro
		enviroment:
			- NODE_ENV=development
```
- In`docker-compose.prod.yml`:
```docker-compose.yml
version: "3"
services:
	node-app: 
		enviroment:
			- NODE_ENV=production
```
- To run:
```CMD
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d
```
- If we want rebuild container:
```CMD
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up -d --build
```

# Sources
- [Video 11 - Docker Practical Course in Arabic](https://youtu.be/sbiArlT5hG8?si=0Mw9GOwtG0RzQhBl)