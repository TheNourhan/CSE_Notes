# Explanation

- To solve security issues of [[Docker Hot Reload#Bind Mount]] (tow way binding) we need too change it to (one way binding).
- **Use a read-only bind mount:**
- Add `:ro` brief of read only.
```CMD
docker run --name express-node-app-container -v $(pwd):/app:ro -d -p 4000:4000 express-node-app
```
- This will reflect any changes from local environment to container only.
- But if we remove `node_modules` for example from the local environment, this will cause a problem.
- To solve this problem we use what they named `anonymous volumes`:
- `-v /app/node_modules` -> The container will not respond to any changes to this path from the local environment.
```CMD
docker run --name express-node-app-container -v $(pwd):/app:ro -v /app/node_modules -d -p 4000:4000 express-node-app
```
- Instead of binding all files inside container and then used `anonymous volumes` we can do that:
- Only listen to files that change significantly, by creating a `src` folder, putting the source code in it, and binding to it `$(pwd)/src:/app/src:ro`.
```CMD
docker run --name express-node-app-container -v $(pwd)/src:/app/src:ro -d -p 4000:4000 express-node-app
```
- To remove all volumes:
```CMD
docker volume prune
```
- To view all volumes:
```CMD
docker volumes ls
```

# Sources
- [Video 8 - Docker Practical Course in Arabic](https://youtu.be/voTvVHAi4fM?si=0qADyEt2a9rG54le)
- [Volumes](https://docs.docker.com/storage/volumes/)