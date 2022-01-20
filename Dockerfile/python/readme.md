
```
# build the image
$ docker build -t myimage .

# list images
$ docker images

# run the container based on our image
$ docker run -d -p 5000:5000 myimage

# test
$ curl http://localhost:5000
```