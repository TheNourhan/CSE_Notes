# Explanation

- We can run different commands in docker-compose based on env:
- In `docker-compose.dev.yml`:
```docker-compose.yml
version: "3"
services:
	node-app: 
		volumes:
			- ./src:/app/src:ro
		enviroment:
			- NODE_ENV=development
		command: npm run start
```
-  In `docker-compose.prod.yml`:
```docker-compose.yml
version: "3"
services:
	node-app: 
		enviroment:
			- NODE_ENV=production
		command: npm start
```
- We can pass an argument to the [[Dockerfile]] to specify which environment to run in.
```Dockerfile
 FROM node:20 
 WORKDIR /app 
 COPY package.json .
 
 ARG NODE_ENV
 RUN if [ "$NODE_ENV" = "production" ]; \
	 then npm install --only=production; \
	 else npm install; \
	fi
	 
 COPY . .
 EXPOSE 4000
 CMD ["npm", "run", "start-dev"]
```
- To send argument from `docker-compose.dev.yml`:
```docker-compose.yml
version: "3"
services:
	node-app: 
		build:
			context: .
			args:
				- NODE_ENV=development
		volumes:
			- ./src:/app/src:ro
		enviroment:
			- NODE_ENV=development
		command: npm run start
```
- To send argument from `docker-compose.prod.yml`:
```docker-compose.yml
version: "3"
services:
	node-app: 
		build:
			context: .
			args:
				- NODE_ENV=production
		enviroment:
			- NODE_ENV=production
		command: npm start
```
## Multi-Stage [[Dockerfile]]:
- We can name stages, by adding an `AS <NAME>`:
```Dockerfile
 /*
 FROM node:20 as base
 FROM base as development
 FROM base as production
 */
 
 FROM node:20 as development
 WORKDIR /app 
 COPY package.json .
 RUN npm install	 
 COPY . .
 EXPOSE 4000
 CMD ["npm", "run", "start-dev"]

 FROM node:20 as production
 WORKDIR /app 
 COPY package.json .
 RUN npm install --only=production	 
 COPY . .
 EXPOSE 4000
 CMD ["npm", "start"]
```
- In `docker-compose.dev.yml`:
```docker-compose.yml
version: "3"
services:
	node-app: 
		build:
			context: .
			target: development
		volumes:
			- ./src:/app/src:ro
		enviroment:
			- NODE_ENV=development
		command: npm run start
```
- In `docker-compose.prod.yml`:
```docker-compose.yml
version: "3"
services:
	node-app: 
		build:
			context: .
			target: production
		enviroment:
			- NODE_ENV=production
		command: npm start
```

# Sources
- [Video 12 - Docker Practical Course in Arabic](https://youtu.be/2-bbh5kmNSc?si=pLnuCrkRoZf2P7-C)
- [Multi-stage builds](https://docs.docker.com/build/building/multi-stage/)