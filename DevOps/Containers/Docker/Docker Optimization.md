# Explanation

1. Do i need to copy all files `COPY . .`?
	- The `docker exec` command runs a new command in a running container.
	- This will be open terminal on container:
	```CMD
	docker exec -it express-node-app-container bash
	```
	- Then we can write `ls` inside container terminal to browse all files and dirs.
	- We don't need to copy `Dockerfile` inside container.
	- We don't need to copy `node_modules` inside container because `RUN npm install` do that.
	- There is file named `.dockerignore` like `.gitignore`, it is specifies which files and directories should be excluded from the build context, preventing unnecessary files from being included in the image.
	```dockerignore
	/node_modules
	Dockerfile
	.env
	docker-compose*
	```
2. Why did we split `package.json` copy command? 
	- If there is no change in `package.json` this step will be cached without repeating it when rebuilding.


# Sources
- [Video 6 - Docker Practical Course in Arabic](https://youtu.be/UDqNwH4VpOU?si=uyetTiY-CT1e9P5K)
- [Docker build cache](https://docs.docker.com/build/cache/)