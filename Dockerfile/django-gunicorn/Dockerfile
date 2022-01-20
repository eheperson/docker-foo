# Base image
FROM Python:3.8

# create and set working directory
RUN mkdir /app
WORKDIR /app

# copy requirements.txt and install requirements
COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

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