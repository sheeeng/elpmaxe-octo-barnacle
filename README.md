# elpmaxe-octo-barnacle

Example

* Build and run Jenkins with Docker.

## Build

```
docker build ./jenkins \
    --tag jenkins:elpmaxe \
    --force-rm \
    --no-cache \
    --pull
```

## Persistent Data Storage

```
mkdir -p /opt/containers/jenkins/jenkins_home
chown -R 1000:1000 /opt/containers/jenkins/jenkins_home
chmod 777 /opt/containers/jenkins/jenkins_home
```

## Run

```
docker run \
    --publish 8080:8080 \
    --publish 50000:50000 \
    --rm \
    --volume /opt/containers/jenkins/jenkins_home:/var/jenkins_home \
    jenkins:elpmaxe
```

## Permissions

- Use `docker exec` to run a command in a running container.

```
docker exec \
    --interactive \
    --tty \
    $(docker ps \
      --quiet \
      --filter=ancestor=jenkins:elpmaxe) \
    /bin/bash
```

- Use `id` inside the container to check user permissions.

```
bash-4.3$ id
uid=1000(jenkins) gid=1000(jenkins) groups=1000(jenkins)
```

- Check user inside the container has sufficient permissions to mounted volume.
