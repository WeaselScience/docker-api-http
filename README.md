This image exposes an http server on port 80, and proxies it to `/var/run/docker.sock`. This means that accessing port 80 on a container running off of this image means accessing the Docker API. No need for Docker Engine configuration changes. However, you do need to mount the host's `/var/run/docker.sock` to this image for it to work.

This image is created to be used internally. To use it, run the image as a standalone container or a service, and assign the container/service to a bridge/overlay network.

Regular:
```
docker network create docker-api;
docker run --net docker-api --name docker-api -v /var/run/docker.sock:/var/run/docker.sock weaselscience/docker-api-http;
# When starting other containers that need access to this, make sure to include "--net docker-api"
# To access from the container which has joined the "docker-api" network, do "curl http://docker-api/v1.31/info"
```

Swarm Mode:
```
docker network create --driver overlay docker-api;
docker service create --net docker-api --name docker-api --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock weaselscience/docker-api-http;
# Modify other services to have access to the API
docker service update --network-add docker-api <service-name>;
# To access from the service which has joined the "docker-api" network, do "curl http://docker-api/v1.31/info"
```
