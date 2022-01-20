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

