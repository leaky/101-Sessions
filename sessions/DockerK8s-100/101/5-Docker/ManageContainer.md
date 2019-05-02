
# Managing Containers

### Stop command
Run a new container:

```docker run -d --name test ubuntu:16.04 /bin/bash```

List the names of the containers:

```docker ps -a```

Stop using the name or id of the newly running container:

```docker stop test```

### Start command

```docker start test```

### Logs of container
Here is a container that will generate some logs

```docker run --name test2 -d busybox sh -c "while true; do $(echo date); sleep 1; done"```

To view the logs of the container as a snapshot, use the following command:

```docker logs test2```

Log outputs can be *followed* to view logs in real time by using the ```-f``` option:

```docker logs -f test2```

### SSH into a Container or Attaching to a running container

Use ```docker ps``` to get the name of the existing container.

Use the following command to open a bash shell inside the container: 
```docker exec -it <container name> /bin/bash```

Generically, use ```docker exec -it <container name> <command>``` to execute whatever command you specify in the container.

```docker run -d --name test nginx```

```docker attach test``` (Attaches local I/O and error streams to a running container)

Be careful as stopping this will stop the container but following command will not stop the container when exiting the shell:

```docker exec -it test bash```
