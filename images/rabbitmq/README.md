# RabbitMQ

## Setup

Pulling the image from the dockerhub

> [!NOTE]
> The image we are pulling that have the management plugin enabled by default.

```
podman pull docker.io/library/rabbitmq:3.13.6-management
```

Create a container and run the image

> [!IMPORTANT]
> One of the important things to note about RabbitMQ is that it stores data based on what it calls the "Node Name", which defaults to the hostname. What this means for usage in Docker is that we should specify -h/--hostname explicitly for each daemon so that we don't get a random hostname and can keep track of our data:
> -- [source](https://hub.docker.com/_/rabbitmq)

> [!NOTE]
> The command below doesn’t attach a persistence volume to the container.
> 
> Use the `-v` if required, for example `-v rabbitmq-3_13_6-data:/var/lib/rabbitmq`

```
podman run -d --hostname my-rabbit --name some-rabbit -p 5672:5672 -p 15672:15672 rabbitmq:3.13.6-management
```

To login

TODO

## Reference

* [dockerhub/rabbitmq](https://hub.docker.com/_/rabbitmq)
