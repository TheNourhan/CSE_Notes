# Explanation

- We can add env variables in Dockerfile:
```Dockerfile
ENV PORT=4000
EXPOSE $PORT
```
- Or in command line `--env PORT=4000`:
```CMD
docker run --name express-node-app-container -v $(pwd)/src:/app/src:ro --env PORT=4000 --env NODE_ENV=development -d -p 4000:4000 express-node-app
```
- To view env variables inside container:
```CMD
docker exec -it my-node-app-container bash
printenv
exit
```
- Or using env file `--env-file ./.env`:
```CMD
docker run --name express-node-app-container -v $(pwd)/src:/app/src:ro --env-file ./.env -d -p 4000:4000 express-node-app
```
- Or using docker-compose:
```docker-compose.yml	
		environment:
			- PORT=4000
			- NODE_ENV=production
		env_file:
			- ./.env
```

# Sources
- [Video 10 - Docker Practical Course in Arabic](https://youtu.be/1mQ8NXcHmGk?si=CmqcmrutYPQv3Kh-)