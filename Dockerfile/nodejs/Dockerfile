# Select OS
FROM node:alpine

# Copy app files into container
#   (create a /app dir in filesystem of that image)
COPY . /app

# Specify working directory in container
#   (all executions will assume we are working in that directory)
WORKDIR /app

# execute a command
CMD node app.js
