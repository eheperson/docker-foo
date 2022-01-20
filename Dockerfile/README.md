# Dockerfile

* **`Dockerfile` tags**
    - `FROM` : it is going to build our image from another pre-existing image
    - `RUN` : it is a command that allows us to do any bash shell command we would do normally.
    - `EXPOSE` : allows us docker image to have a port or ports exposed to outside the image. This is important for web applications and software we want to receive requests.
    - `CMD` : It is the final command our docker-image will run.  It is typically reserved for something like running a web application.
    - `COPY` : It allows us to copy local files to our Docker image.


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