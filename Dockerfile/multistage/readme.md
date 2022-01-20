

* Although this may not be really useful during development time, we cover it quickly as it is interesting for shipping the containerized Python application once development is done. 

* What we seek in using multi-stage builds is to strip the final application image of all unnecessary files and software packages and to deliver only the files needed to run our Python code.  


* Notice that we have a two stage build where we name only the first one as builder. 
    - We name a stage by adding an AS `<NAME>` to the `FROM` instruction 
    - And we use this name in the `COPY` instruction where we want to copy only the necessary files to the final image.

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