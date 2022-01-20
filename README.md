# Docker

Docker is a platform for building, running and shipping applications

Once you are done installing Docker, test your Docker installation by running the following: `docker run hello-world`

## Development workflow when using Docker

Step 1: Create an application in any language\
Step 2: Create a Dockerfile\
Step 3: Dockerize application using Dockerfile to create an image\
Final : Start a container using created image\

    ----Application----|
                       |---> Dockerizing(packing) ---> Image
    ----Dockerfile-----|

* **Dockerfile :** It is a plaintext fileincludes instructions that docker uses to packageup our app into an image

* **`Dockerfile` tags**
    - `FROM` : it is going to build our image from another pre-existing image
    - `RUN` : it is a command that allows us to do any bash shell command we would do normally.
    - `EXPOSE` : allows us docker image to have a port or ports exposed to outside the image. This is important for web applications and software we want to receive requests.
    - `CMD` : It is the final command our docker-image will run.  It is typically reserved for something like running a web application.
    - `COPY` : It allows us to copy local files to our Docker image.

* **Docker in Action**
    ```
    mkdir docker-test
    cd docker-test
    touch app.js
    echo "console.log('enivicivokki');" >> app.js
    brew install node

    echo Dockerfile

    # Select OS
    echo "FROM node:alpine" >> Dockerfile

    # Copy app files into container
    #   (create a /app dir in filesystem of that image)
    echo "COPY . /app" >> Dockerfile

    # Specify working directory in container
    #   (all executions will assume we are working in that directory)
    echo "WORKDIR /app" >> Dockerfile

    # execute a command
    echo "CMD node app.js" >> Dockerfile

    # build an image
    # docker build -t <image_name> <Dockerfile_location>
    docker build -t docker-test .

    # Start a docker container using builded image
    docker run docker-test
    ```

    ```
    $ mkdir django-docker
    $ cd django-docker
    $ python3 -m venv venv
    $ source venv/bin/activate
    $ pip install Django
    $ django-admin startproject core .
    $ pip freeze >> requirements.txt
    $ touch .dockerignore
    $ echo "./venv" >> .dockerignore
    $ touch Dockerfile
    $ nano Dockerfile 
    $ docker build -t django-docker -f Dockerfile .
    $ docker run -it -p 80:8888 django-docker

    Dockerfile
        FROM python:3.9-slim-buster
        ENV PYTHONBUFFERED 1

        RUN mkdir /app
        WORKDIR /app

        COPY requirements.txt requirements.txt
        RUN pip3 install -r requirements.txt

        COPY . .

        CMD ["python3", "manage.py", "runserve", "0.0.0.0:8000]
    ```

    ```
    $ mkdir django-docker
    $ cd django-docker
    $ python3 -m venv venv
    $ source venv/bin/activate
    $ pip install Django
    $ pip install gnuicorn
    $ django-admin startproject core .
    $ python manage.py makemigrations
    $ python manage.py migrate
    $ python manage.py createsuperuser
    $ gnuicorn core.wsgi:application --bind 0.0.0.0:8000
    $ touch .dockerignore
    $ echo "./venv" >> .dockerignore
    $ touch Dockerfile
    $ nano Dockerfile 
    $ docker build -t django-docker -f Dockerfile .
    $ docker run -it -p 80:8888 django-docker
    # then > 'http://localhost'
    
    Dockerfile
        # Base image
        FROM Python:3.8

        # create and set working directory
        RUN mkdir /app
        WORKDIR /app

        # add current directory content to working directory
        ADD . /app

        # set default env variables
        # grab these variables via python's os.environ
        ENV PYTHONBUFFERED 1
        ENV LANG C.UTF-8
        ENV DEBIAN_FRONTEND:noninteractive
        ENV PORT:8000

        # install system dependencies
        RUN apt-get update && apt-get install -y --no-install-recommends\
            tzdata python3-setuptools python3-pip python3-dev\
            python3-venv git && apt-get clean &&\
            rm -rf /var/lib/apt/lists/*

        # install environment dependencies
        RUN pip3 install --upgrade pip
        RUN pip3 install pipenv

        #install project dependencies
        RUN pipenv install --skip-lock --system --dev

        EXPOSE 8888
        CMD gnuicorn core.wsgi:application --bind 0.0.0.0:8000
    
    ```

## Docker project analogy based on django app

**Steps :**
- Create a new django app
- Prepare a Django app for docker
- Build a docker image
- Start a new Docker Container

    ```
        Django App  > Docker Image > Docker Container 
        ----------    ------------   ----------------
        django_app    django_app      OS
                      Dockerfile      Database
                                      django_app
                                      packages
    ```

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

## Example Code
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
- `$ docker rm $(docker images -q)` : to remove all images

## Playing with Busybox

``` 
# Pull the busybox image
docker pull busybox

# Run the busybox image
docker run busybox

# Run the busybox with command
docker run busybox echo "hello from busybox"

```


## Example docker project structure

    compose-web-app
    │
    ├── .git/
    ├── .gitignore
    ├── .dockerignore
    ├── venv/
    ├── main
    │   ├── webapp/
    │   ├── manage.py
    │   ├── requirements.txt
    │   ├── Dockerfile.prod
    │   ├── Dockerfile.dev
    │   └── entrypoint.prod.sh
    └── Readme.md

# DOCKER-COMPOSE
docker-compose is a tool for defining and running multicontainer apps.\
With a single command, we can then build all images and run all containers.\
Compose revolves around a config file called `docker-compose.yaml`. In this we define all our services

**Services :** Think of a service as a part of our application; a database or API for example. All our services rely on an image with which we create a container.

* When we spin up our containers with docker-compose, it defines a network that all our services share.

**Using Environment Variables**
- Runnig our containers can be made more flexible with environment variables.
- ".env" file will be used to create and use environment variables.


* **`docker-compose.yaml` tags**
    - `container-name` : The name we will give our container. Otherwise a random name will be generated.
    - `hostname` : Our container will be accessible on the internal network by this hostname.
    - `image` : The software that's going to get installed in the container.
    - `environment` : Setting sfor the container.
    - `ports` : For example, by default we cannot reach the database in our container. With this port mapping we can patch through access to the database.
        - `<port_to_host> : <port_to_container>` 
        - `xxxx:xxxx`
    - `restart` : What happens if our container crashes
        - `unless-stopped`
        - `always`
        - `no`
        - `on-failure`
    - `build` :
        - `context` : Referring to folder which contains a dockerfile
        - `dockerfile` :Specifiyng a dockerfile
        ```
            build: 
                context: .
                dockerfile: Dockerfile
        ```
    - `volumes` : volumes are a way to persist data.
        - when we run our image, our database gets build in the container and, we can put some data in it.
        - if we remove our container our data is gone as well.
        - Volumes allows us to copy the data in our container to our host.
        - Volumes can also be shared by multiple containers
        - We can also put our source-code in volumes so that when we edit the code on our host, the change gets reflected in the container.
        ```
            # example usage for volumes tag
            volumes:
                - ./beersnob.api/src/:/usr/src/app
                - /usr/src/app/node-modules
            
            # We mirror our source-code into the container.
            # If we change anything in our source-code in the host, the changes gets reflected in the container once we re-run it.
        ```
    - `depends-on` : start this container once the containers is up and running defined under this tag.

## Example docker-compose project structure

    compose-project
    │
    ├── test_api
    │   ├── Dockerfile
    │   └── api files
    │
    ├── test_database
    │   ├── Dockerfile
    │   └── app files
    │
    └── docker-compose.yaml

