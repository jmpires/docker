# Create a VM with KVM
# Update the OS

# Install Docker
# Install pip

# Pull from the Ubuntu image
# FROM ubuntu:16.04

# Need to install this version as pip is not working in the ubuntu:16.04
FROM python:2.7-slim

# Make a folder to store the app source code and setting the working directory
RUN mkdir /app
WORKDIR /app

# Simple copy command of the requirements file. No path because currently is in the same location
COPY requirements.txt requirements.txt

# Install python dependencies
RUN pip install -r requirements.txt

# Copying the application source code
COPY . .

# Passing a key and a value (Labels are optional and are like Tags that can be filter by)
LABEL maintainer="Jorge Pires <jorgepires.email@gmail.com>"
LABEL version="1.0"

# Defines the default command that will be run when the current image will be started
CMD flask run --host=0.0.0.0 --port=5000

# Install the apache web server

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get install -y apache2

# Adding some content for Apache server
RUN echo "This is a running Ubuntu test docker" > /var/www/html/index.html

# Copying setting file & adding content to the apache web server
COPY data/httpd.conf /etc/apache2/httpd.conf

# Install the haproxy and running needed actions
RUN apt-get install -y haproxy rsyslog
RUN rm -rf /var/lib/apt/lists/*
RUN mkdir /run/haproxy

COPY data/haproxy.cfg /etc/haproxy/haproxy.cfg

# Starting the rsyslog (4 logs) & haproxy (proxy) services
CMD service rsyslog start && haproxy -f /etc/haproxy/haproxy.cfg && tail -F /var/log/haproxy.log




# Run command test was: docker container run -it -p 5000:5000 -e FLASK_APP=app.py faro
# It was expected that when accessing to the browser with "localhost:5000" we will get a value of 0
# We didn't get the expected because of a issue in the configuration of the haproxy that we still are investigating

# Weakness of the Dockerfile image:
# The docker image should be tested first in the dev, then in stg and only after be in production after all the bugs and/or security problems have been addressed;
# Also the Dockerfile should be part of a secure repo and as also the additional support files;
# Dockerfile  should be in a CI/CD pipeline to be managed and updated in a more Agile way by all the maintainers;




# Defining a command to be run after the docker is up
# operation ping -> google.com

# ENTRYPOINT ["ping"]
# CMD ["google.com"]
