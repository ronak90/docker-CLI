# docker-CLI

https://dev.to/tanmoysarkar/docker-cli-yaml-in-one-shot-3n90

Dockerfile

It's just a text file that contains instructions for building a Docker image.

It's just to automate the process that you do manually. So if you know how to do a process manually, you can learn it quickly.
Format

INSTRUCTION arguments

Instruction Set

In the below table, I have mentioned some sort terms. dir -> Directory, src -> Source, dst -> Destination
INSTRUCTION 	DESCRIPTION
FROM <image_name> 	Fetch base image for Docker
COPY <src_dir_host> <dest_dir_container> 	Copy a folder of the host system to the container
WORKDIR <dir_path_contaiiner> 	Set the working directory of the container where the commands will run
RUN <command> 	Run commands in a shell
RUN [<command arg1>, <command arg2>] 	We can break the command in command args also.
Ex : RUN "apt-get update" -> RUN ["apt-get", "update"] 	
ENV <key>=<value> 	Set environment variables
EXPOSE <container_port> 	Expose the port of a container to make it accessible in the same network
ENTRYPOINT <command> 	That command will execute as soon as the container boot up
ENTRYPOINT [<command arg1>, <command arg2>] 	We can break the command in command args also.
Ex : RUN "/bin/sh sample.sh" -> RUN ["/bin/sh", "sample.sh"] 	

There is one more command, which you see mostly. CMD

The purpose of this command is to run the commands specified in arguments. It also has two formats, for example.

    CMD echo "hello-world."

    CMD ["/bin/sh", "echo", "hello-world"]

You might be confused now about the difference between RUN and CMD.

    RUN runs all the commands specified in the argument

    For CMD there is some particular case.
        If you have provided some commands to run in docker run command, CMD is going to be ignored.
        If you have listed multiple CMD statements, only the last CMD will be executed.
        IF ENTRYPOINT in Dockerfile is provided, CMD it is going to be ignored.
        In any container deployment platform, you can see the CMD to run manually.

🔵 As the blog's purpose is to give concise details of Dockerfile and CLI, we are not attaching Dockerfile examples here. But will create some blogs on Dockerfile and attach links to them.
Docker CLI
Arguments List

Argument
	

Description

-u
	

Username

--name
	

Name [Normally used for container]

-d
	

Detach [Run in the background]

-a
	

All [Stopped + Paused + Running]

-i
	

Interactive

-t
	

- tty [stdin] [For Container]
- tag name [For Image]

-it
	

Interactive with stdin

-w
	

Working directory [example -w '/opt/test']

-p
	

Port [Example : -p <host_system_port>:<container_port> ]

-v
	

Volume Mount [Example : -p <host_system_volume_path>:<container_volume_path> ]

-e
	

Environment Variable [Example : -e <variable_name>=<value> ]
Image Specific Commands

List all local images

docker images

Build Image From Dockerfile in current directory

docker build . -t <tag_name>

Pull an image from Dockerhub

docker pull <image_name>
# example : docker pull redis

Delete an image

docker rmi redis

Remove all unused images

docker image prune

Container Specific Commands

Run a docker container from an image

docker run <image_name>

    Now you can refer the Arguments List table to choose your required arguments

    I am solving an question for example.

    Let's assume, I need to create an container from image of redis with port mapping from container port 6379 to host port 6379 . The name will be redis-instance-1 . Make the instance detachable & run redis-server --requirepass "SECRET_PASSWORD" at its beginning.

    docker run --name redis-instance-1 -d -p 6379:6379 redis redis-server --requirepass "SECRET_PASSWORD"

        Its important to notice that , you need to pass all the arguments before providing the image name and entrypoint_command

List containers [only Running]

docker ps

List all containers [Stopped + Paused + Running]

docker ps -a

Start or Stop a container

docker start|stop <container_name or container_id> 

    You can get the Container ID by running the command for list all container

Remove a stopped container

docker rm <container_name or container_id>

Attach to the current process of container

docker attach <container_name or container_id>

Run a command in the container

docker exec <container_name or container_id> <command>

    Example : Start a bash terminal in redis instance

    docker exec -it redis /bin/sh

❓You may have a question. What's the difference between exec and attach, then

With attach, we attach to the process that's currently running in the container

But with exec, we can run a new process in a container without hampering the running process of the container

Log the data of the current process of the container

docker logs -f <container_name or container_id>

Inspect and grab all the details of a container

docker inspect <container_name or container_id>

    It will return the details in an JSON format

Check the stats [CPU, RAM, Network, Storage usage] for all running containers

docker container stats

