# Redis

## Setup

Pulling the Redis image from the dockerhub

```
podman pull docker.io/library/redis:7.2.5
```

Create a container and run the image

```
podman run --name redis-7_2_5 -d -p 6379:6379 -v redis-7_2_5-data:/var/redis/data redis:7.2.5 --requirepass dev
```

Breaking down the command

| Flag            | Value                              | Description                                                                                                          |
| --------------- | ---------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `--name`        | `redis-7_2_5`                      | assigns a descriptive name to the container.                                                                         |
| `-d`            |                                    | runs the container in detached mode.                                                                                 |
| `-p`            | `6379:6379`                        | maps port 6379 from the container to port 6379 on the host, enabling external access to Redis.                       |
| `-v`            | `redis-7_2_5-data:/var/redis/data` | create a volume called `redis-7_2_5-data` if not exist and map the volume to the `/var/redis/data` of the container. |
| `--requirepass` | `dev`                              | set the Redis password to `dev`. Note this flag belongs to Redis.                                                    |

To start after exist

```
// find the container ID.
podman ps --all

// then start the container by ID
podman start container-id
```

To stop

```
podman start container-id
```

Note that the port cannot be changed once the volume created.

## Reference

* [Using systemd to control the startup of Podman containers](https://podman.io/blogs/2018/09/13/systemd#:~:text=podman%20pull%20docker.io%2Fredis%20sudo%20podman%20run%20-d%20--name,CONTAINER%20ID%20IMAGE%20COMMAND%20CREATED%20STATUS%20PORTS%20NAMES)
