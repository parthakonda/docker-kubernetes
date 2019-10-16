# This is to help the commands regarding docker


## Running a container from an image
```
{docker} {run} {image-name}
```
`docker` - nothing but your docker client<br>
`run` - command to create and run the container<br>
`image-name` - name of the image<br>

Example:
```
docker run hello-world
```


## Overriding a default command for docker
```
{docker} {run} {image-name} {command-to-execute}
```
`docker` - nothing but your docker client<br>
`run` - command to create and run the container<br>
`image-name` - name of the image<br>
`command-to-execute` - default command to override

Example:
```
docker run busybox ls
```

## List all running container
```
{docker} {ps}
```
`docker` - nothing but your docker client<br>
`ps` - list's all the containers that are running<br>

Note: This will show the containers which are running right now only.

## List all containers that are created so far
```
{docker} {ps} {--all}
```
or 
```
{docker} {ps} {-a}
```
`docker` - nothing but your docker client<br>
`ps` - list's all the containers that are running<br>
`--all` - this will enabled to show the history also
`-a` - equivalent to `--all`

## Container life-cycle
When we run(docker run <image>) then it actually consists of 2 things.
1. Create the container from image
2. Start container using it id

1. Create the container from image
```
docker create <image_name>
```
The above will generate a random id for the container.

2. Start container using it id
```
docker start <container_id>
```

Note: The above will execute the container, however the output won't be redirected to console.
In order to get the output to the console we need to append an option i.e., `-a`

```
docker start -a <container_id>
```

## Removing stopped containers
When you run docker run <some_image> then once it got executed the container will only get exited. But it is still occupying space.
```
docker system prune
```

prune - this will do the following things.
- Removes the stopped containers
- Removes the networks which are not used at-least one container
- All dangling images
- All build cache


## Get logs from a container
Instead of specifying -a to the start command, you can actually use command called `logs` to get the logs emitted by the container.

```
docker logs <container_id>
```
Note: The above won't re-run the container. It will just show the log of it.