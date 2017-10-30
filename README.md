Regular:
```docker run --name docker -p 80:80 -v /var/run/docker.sock:/var/run/docker.sock weaselscience/docker-api-http```

Swarm Mode:
```docker service create --name docker --publish 80:80 --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock weaselscience/docker-api-http```
