# Docker

Docker is a platform that uses containers to package software and
its depencies into a light and isolated environment

## Key Terms

### Container

A lightweight, standalone, and executable software package that includes everything needed to run a piece of software  
or  
An isolated process in a machine that can contain an application and all its necessary dependencies. Isolated filesystems provided by an image  
**_Each container should do one thing and do it well_**  
\*\*\*\*\*\*\*\*\*\*

### Context

A specific environment where Docker operates and performs actions. Similar to a BE(Boot Environment) has the exact rules, settings, and configurations/conditions needed by the app.  
The configuration and settings for Docker to interact with different container env_ Examples: local Docker install, remote Docker host, or a cloud-based container service like AWS ECS or kubernetes.  
\*\*\*\*\*\*\*\*\*\*

### Volumes

Map specific filesystem path on local machine to the container for persistent data  
_Named Volumes:_ Bucket of data. Docker maintains the physical location on the disk. End user names only needs to remember the name of the volume  
_Bind Mounts:_ We control the exact mountpoint on the host. Can be used to persist data or more often to provide additional data inst containers.  
\*\*\*\*\*\*\*\*\*\*

### Image

A template of a container's filesystem. It has everything needed to run the application - all dependencies,configuration, scripts, binaries, etc.  
Also has it's own configuration stored like env vars  
\*\*\*\*\*\*\*\*\*\*

### Environment variables

A default command to run on other metadata  
\*\*\*\*\*\*\*\*\*\*

### Tags

Giving it a unique name and version to be easily identifiable and allows others to pull specific version
\*\*\*\*\*\*\*\*\*\*

### Network

Provides a way for containers to communicate with each other in a virtual network environment. If two containers are on the same network, they can talk to each other. If they aren't, they can't.  
network alias are assigned as a more descriptive name for containers to use when communicating with one another.  
\*\*\*\*\*\*\*\*\*\*

---

## Getting Started

### COMMAND

``  
`-`  
\*\*\*\*\*\*\*\*\*\*

### See all Docker images

`docker images`  
\*\*\*\*\*\*\*\*\*\*

### See docker image history

`docker image`
`history <img> --no-trunc` See the layers in the image untruncated
\*\*\*\*\*\*\*\*\*\*

### Build docker image

`docker build -t <image_name>:<tag> <path_to_docker_file>`  
`-t` name for the image  
`-f <path to docker file>`  
\*\*\*\*\*\*\*\*\*\*

### See all containers running and not running

`docker ps -a`  
`-a` show all containers  
\*\*\*\*\*\*\*\*\*\*

### Run docker compose file

`docker compose <action>`
`up`  
`down` Tear down containers  
`-d` detached
\*\*\*\*\*\*\*\*\*\*

### Create and run a container

`docker run --name <name> <image>:<version> `

`-d` detached mode running container in the background  
`-p` map port of x of the host to port y in the container  
`--rm` remove container when stopped  
`-v <volume_name_or_absolute_path>:<cntner_pth>` Will created named volume if not already created  
`-w <working_directory>` sets the container present working directory where the command will run from
`-e` Set environment variables for the container  
`--network <network_name>` Connects container to specific docker network  
`--network-alias <cntnr_alias>` Assigns additional alias to a container when connected to a network. An alternative name other containers can refer to the container.  
`<optional_corresponding_interprt> <optional_cmnd>` command to run on container
`<username>/<repo_name>` Can include the user and the repo of that user you want to pull an image from instead of `<image>:<version>`  
`<optional_interprt> <optional_cmnd>` command to be ran in the container
example: `bash -c "echo Hello!"` | `sh -c "echo Hello!` | `python /path/to/your/project.py`  
_Example_

```bash
docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started

docker run -dp 3000:3000 \
    -w /app -v "$(pwd):/app" \
    node:18-alpine \
    sh -c "yarn install && yarn run dev"
```

\*\*\*\*\*\*\*\*\*\*

### Rename a container

`docker rename <og_name> <new_name>`  
` `  
\*\*\*\*\*\*\*\*\*\*

### Start Docker container

`docker start <container>`  
`-i` interactive  
\*\*\*\*\*\*\*\*\*\*

### Stop Docker container

`docker stop <container>`  

\*\*\*\*\*\*\*\*\*\*

### Delete the container

`docker rm <container_name_or_id>`  
`-f` forcefully stop the container if running and then delete it

\*\*\*\*\*\*\*\*\*\*
---

### Container logs

`docker logs -f <container_name_or_id>`
`<container_name_or_id>` optional can show logs of all containers  
`-f` Follow log output

---

## Advanced

### Creating network

`docker network <action>`  
`create <network_name>`  
`inspect` see network info  
`ls` see list of networks  
\*\*\*\*\*\*\*\*\*\*

### Volume

`docker volume <action>`  
`create <name_volume>`  
`inspect` see info of volume  
`ls` see list of volumes  
\*\*\*\*\*\*\*\*\*\*

### Execute a command into a container

`docker exec <container> <command>`  
`-i` interactive. Keep STDIN open even when unattached  
`-t` Allocate a pseudo-TTY(emulation of a physical terminal)
_Example:_  
`docker exec -it 56a714cded3b /bin/bash` open an interactive session with a pseudo-TTY pointing to the shell intrepeter /bin/bash  
`docker exec 56a714cded3b cat /data.txt`  
\*\*\*\*\*\*\*\*\*\*

### Create a tag for an existing docker image

`docker tag <image name>:<optional_tag> <YOUR-USER-NAME>/<repo name>`  
\*\*\*\*\*\*\*\*\*\*

### Push docker image into Docker hub repo

`docker push <username>/<image_name>:<optinal_tag>`

\*\*\*\*\*\*\*\*\*\*

### Change the environment where Docker operates

`docker scout <action> <image>`  
`cves <img1>` Display CVEs (Common Vulnerabilities and Exposures) identified in an image
`quickview <img1>` Quick overview of an image
`compare <img1> <img2>` compare two images and display differences  
`recommendations` Display available base image updates and remediation recommendations
\*\*\*\*\*\*\*\*\*\*

### Change the environment where Docker operates

`docker context create ecs myecscontext`  
` `  
\*\*\*\*\*\*\*\*\*\*

## Configs

### Docker Image file

A docker file defines the configuration and instructions for building a docker container image  
The file is named _Dockerfile_

```yaml
FROM <base_image>
WORKDIR <working_dir_on_container>
ADD <path_of_local_file_to_add> <path_on_cntnr_to_save_file>

```

### Docker Compose file

Defines the configuration of multiple containers in one file. Define and share multi-container applications.  
_docker-compose.yml_

```yaml
services: #list of services/containers we want to run
  <service_name_(app)>: # The name will automatically become a network alias
    image: node:18-alpine
    container_name: bless #if name is not specified it will default to: <project-name>_<service-name>_<replica-number>
    command: sh -c "yarn install && yarn run dev"
    ports:
      - 3000:3000
    working_dir: /app
    volumes:
      - ./:/app
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: secret
      MYSQL_DB: todos

  <service_name_(mysql)>:
    image: mysql:8.0
    volumes: # Named volumes are not automatically created in docker compose file like cli
      - todo-mysql-data:/var/lib/mysql
    environment: 
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: todos

volumes: #need to define the volume in the top-level
  todo-mysql-data: #only providing volume name will use default options
```

---

## Processes

### Sharing an App

1. Create an image
2. Test image and create a container
3. Upload image to Docker Hub  
   a. Create repo
   b. Tag image  
   c. Push image

\*\*\*\*\*\*\*\*\*\*
---

## Images

[nginx]()  
[mysql:8.0]()  
[node]()  
[python:3]()  
[nicolaka/netshoot](https://github.com/nicolaka/netshoot)  
useful for troubleshooting or debugging networking issues.  
-

\*\*\*\*\*\*\*\*\*\*
---

## Links

[Docker tutorial](https://docs.docker.com/get-started/02_our_app/)  
[Play with Docker](https://labs.play-with-docker.com/#)  
[Docker CLI](https://docs.docker.com/engine/reference/commandline/cli/)  