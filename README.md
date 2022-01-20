# Docker

Docker is a platform for building, running and shipping applications

Once you are done installing Docker, test your Docker installation by running the following: `docker run hello-world`

## Development workflow when using Docker

**Steps :**
Step 1: Create an application in any language\
Step 2: Prepare app for Docker (Create a Dockerfile)\
Step 3: Build a Docker image (Dockerize application using Dockerfile to create an image)\
Final : Start a container using created image\

    ```
        Django App  > |Dockerizing| > Docker Image > |Start Container| > Docker Container 
        ----------                    ------------                       ----------------
        django_app                     django_app                         OS
                                       Dockerfile                         Database
                                                                          django_app
                                                                          packages
    ```

* **Dockerfile :** It is a plaintext fileincludes instructions that docker uses to packageup our app into an image

## Terminology
* **Images :**  The blueprints of our application which form the basis of containers.
* **Containters :** Created from Docker images and run the actual application.
* **Docker Daemon :** The background service running on the host that manages building, running and distributing Docker containers.
* **Docker Client :**  The command line tool that allows the user to interact with the daemon. 
* **Docker Hub :** A registry of Docker images.

## Docker Commands
* `docker pull <image_name>` : The pull command fetches the busybox image from the Docker registry and saves it to our system.
* `docker images` : You can use the docker images command to see a list of all images on your system.
* `docker image ls` : To see al images on computer
* `docker run <image_name>` :  To run a Docker container
* `docker run -it <image_name>` : Running the run command with the -it flags attaches us to an interactive tty in the container.
* `docker ps` : The docker ps command shows you all containers that are currently running.
* `docker ps -a` : So what we see above is a list of all containers that we ran. 
* `docker start <container_name>` : To run a container
* `docker stop <container_name>` : To stop a container

* Common procedure : 
    ```
    # To download an image 
    docker pull <image_name>

    # To create a container using downloaded image
    docker run <image_name>


    ```

## Most Common Docker-CLI Commands
- `$ docker run -d -p 80:80 docker/getting-started`
    - `-d` : run the container in detached mode (in the background).
    - `-p 80:80` : map port 80 of the host to port 80 in the container.
    - `docker/getting-started` : the image to use.

- `$ docker build -t docker-test -f Dockerfile .`
    - `-t` : tag to specify image_name 
    - `-f` : tag to specify Dockerfile location

- `$ docker run -d -t docker-test`
    - `-d` : means run at background

- `$ docker run -i -t docker-test`
    - `-i` : means interactive mode on

- `$ docker run -it docker-test /bin/bash`
    - `/bin/bash` : to access our docker container's bash shell

- `$ docker rm $(docker ps -a -q)` : to remove all images
- `$ docker rm $(docker ps -a -q)` : to remove all images

## Playing with Busybox

``` 
# Pull the busybox image
docker pull busybox

# Run the busybox image
docker run busybox

# Run the busybox with command
docker run busybox echo "hello from busybox"

```


