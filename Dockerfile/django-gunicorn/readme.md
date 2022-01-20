
* **admin page**
    - username : admin
    - password : admin

```
    $ docker build -t django-docker -f Dockerfile .
    $ docker run -it -p 80:8888 django-docker

    # then > 'http://localhost'
```