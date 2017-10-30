Regular:
```docker run --name docker -v /var/run/docker.sock:/var/run/docker.sock weaselscience/docker-api-http```

Swarm Mode:
```docker service create --name docker --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock weaselscience/docker-api-http```
