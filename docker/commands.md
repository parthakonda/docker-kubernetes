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


## Stopping a container
We can stop the container which is in running can be done using 2 commands.

using `stop`
```
docker stop <container_id>
```
When you're using stop command then it actually sends the HARDWARE signal called SIGTERM to the container. This will make the application/process to listen to those signal and do some actions accordingly. So we can call this as graceful exit. When we issue this `stop` command then docker will wait for `10seconds` to stop the container. If it exceeding more than `10seconds` then it is invoking `kill` command.

using `kill`
```
docker kill <container_id>
```
When you're using stop command then it actually sends the HARDWARE signal called SIGKILL to the container. This will make the application/process to be exited immediately. So we can call this as force exit.


## Executing comamnds in running container
While container is running, if we want it execute some commands then we can use `exec` command along with option called `-it`.

```
docker exec -it <container_id> <your_command>
```

Note: Wihout specifying option `-it` also it will execute the commands but you can't give the input to it.
Whenever a container is spawned then 3 communication channels such as StdIn, StdOut, and StdErr will be attached to the container. 

StdIn - To communicate into the container
StdOut - To pass the output from container to HOST
StdErr - To pass all the error information in the container to the HOST

`-i` represents the StdIn
`-t` represents the prettifying the output. If you don't specify this then your output will not be formatted enought.

So, `-t` is optional.


## Gettind a command prompt/terminal from docker
While working with container, it is quite common that we will be needing shell of the container to play with some. 

```
docker exec -i -t <container_id> <shell_interpreter>
```

```
docker run -it <image_id> <command>
```