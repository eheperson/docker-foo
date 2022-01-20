
build an image
```
    #docker build -t <image_name> <Dockerfile_location>
    $ docker build -t docker-test .
```

Start a docker container using builded image
```
    docker run docker-test
```