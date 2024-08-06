# Explanation

- If we have in `package.json`:
```json
"scripts": {
"start": "node index.js",
"start-dev": "nodemon index.js"
}
```
- We can do this:
```Dockerfile
CMD ["npm", "run", "start-dev"]
```
- Instead of this:
```Dockerfile
CMD ["npm", "start"]
```
- To see logs of container:
```CMD
docker logs express-node-app-container
```
- If we change any file we will need to rebuild a new image and rerunning a new container.
- But if we work on local environment we need to sync between local directory and container.
## Bind Mount:
- Add what they named **bind mount** (tow way binding) `-v $(pwd):WORKDIR` or `%cd%:WORKDIR` on windows :
```CMD
docker run --name express-node-app-container -v $(pwd):/app -d -p 4000:4000 express-node-app
```
- When you use a bind mount, a file or directory on the host machine is mounted into a container. 
-  The file or directory is referenced by its absolute path on the host machine.
- **This will cause security issues, if we remove a file from the container, it will remove a file from the local environment as well.**

# Sources
- [Video 7 - Docker Practical Course in Arabic](https://youtu.be/iT5OjRX9UkM?si=S-tdoIvyaIH4LJUb)
- [Bind Mounts](https://docs.docker.com/storage/bind-mounts/)