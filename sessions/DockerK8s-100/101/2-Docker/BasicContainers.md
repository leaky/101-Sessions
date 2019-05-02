# Basic Containers
## Run Switch Docker CLI commands
### Interactive with Console

To run a container locally and interact with a terminal use ```-i and -t``` switch. 
This can be combined to ```-it```

```docker run -it ubuntu bash```

to exit the bash terminal use ```exit```
Notice that run command can run specific command on the container on start, here its the ```bash``` command.

### Destroy the container afterwards
Often you wish to run a container and then destroy it. This happens a lot when editing and changing your containers in dev. You can use the ```--rm``` option to do this.

```docker run -it --rm ubuntu bash```

### Image names, Repositories and DockerHub

The run command takes a string as a parameter, the above example used ```ubuntu``` this is the key for the image that will be used to run a container. It will look for the image locally first and then default to DockerHub.

```https://hub.docker.com```

You can change the location of where docker looks for an image. This is often an internal vetted repository of images that are approved for your use within an organisation.

Example: the following command will fetch the latest version of ```Mongo```

```docker run mongo```

use ```control-c``` to exit

### Detached Mode

In the real world you don't want to keep a terminal session open for the active container. By using the ```-d``` option, you can detach the container to run in the background and so it's output is not displayed:

```docker run -d mongo```

then run

```docker ps -a```

You should see the container running.

### Stop/Remove containers and Remove images

At this stage you will have to tidy up your docker environment.

Firstly, stop all running containers.

#### Containers

```docker stop my_container```

or to stop all running containers

```docker stop $(docker ps -q)```

or if you really need to kill all

```docker kill $(docker ps -q)```

then you can remove them all

```docker rm $(docker ps -a -q)```

#### Images
```docker images```

```docker rmi my_image```

or, to delete all local docker images run:

```docker rmi $(docker images -q)```

### Versions, Tags and Names

In addition to the name of the docker image you can specify a version and or a tag. 

```docker run -it --rm mcr.microsoft.com/dotnet/core/samples:aspnetapp```

You can also give a name to the container using the ```--name```

```docker run -it --rm --name aspnetcore_sample  mcr.microsoft.com/dotnet/core/samples:aspnetapp```

### Port Mapping, Host to Container 

It's time to combine a number of commands that we have looked at in the session so far, with the introduction of a new option. Here we'll use the ```-p``` option to map a port from the host to the container.

Adding ```-p 8000:80``` to our docker command will map the ports we need for the session and allow us to use a local web browser to view the containerised hosted web sever. 

```docker run -it --rm -p 8000:80 --name aspnetcore_sample mcr.microsoft.com/dotnet/core/samples:aspnetapp```

Note: Windows hosts might need to use the ip address of the container by using the ```docker exec aspnetcore_sample ipconfig``` command in a separate terminal session.

The above command runs an interactive terminal session which will remove itself when it exits. The container will be named "aspnetcore_sample", sourced with key "mcr.microsoft.com/dotnet/core/samples" and be filtered using the tag ```aspnetapp```. 
