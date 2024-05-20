# MYSQL

Pull from dockerhub

```
podman pull docker.io/library/mysql:8.0.32
```

Run the mysql:8.0.32

```
podman run --name mysql-8_0_32 -e MYSQL_ROOT_PASSWORD=db_root_pwd -d -p 3306:3306 -v mysql-8_0_32-data:/var/lib/mysql mysql:8.0.32
```

Breaking down the command

| Flag     | Value                              | Description                                                                                                          |
| -------- | ---------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `--name` | `mysql-8_0_32`                     | assigns a descriptive name to the container.                                                                         |
| `-e`     | `MYSQL_ROOT_PASSWORD=db_root_pwd`  | sets the root password for MySQL.                                                                                    |
| `-d`     |                                    | runs the container in detached mode.                                                                                 |
| `-p`     | `3306:3306`                        | maps port 3306 from the container to port 3306 on the host, enabling external access to MySQL.                       |
| `-v`     | `mysql-8_0_32-data:/var/lib/mysql` | create a volume called `mysql-8_0_32-data` if not exist and map the volume to the `/var/lib/mysql` of the container. |

To start after exist

```
// find the container ID.
padman ps --all

// then start the container by ID
podman start container-id
```

Note that the port cannot be changed once the volume created.
