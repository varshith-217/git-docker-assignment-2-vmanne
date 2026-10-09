# Git and Docker Starter Application

This repository contains a small Python web application used to practice Git, GitHub, and Docker workflows.

## Application

The application listens on port 8000 and returns a text response when accessed over HTTP.

## Verification

The running application should be verified using an HTTP request to port 8000.

## Docker Usage

Build the image:

    docker build -t git-docker-app:test .

Start the application:

    docker run -d --name app-test -p 8080:8000 git-docker-app:test

After the server starts, verify the response:

    curl http://localhost:8080

The response includes the application name, Status: healthy - vmanne,
the welcome message, and Version: 1.0.

View logs and remove the container:

    docker logs app-test
    docker stop app-test
    docker rm app-test

## Container Network Verification

Create a network and start the application on it:

    docker network create app-net
    docker run -d --name app-test --network app-net git-docker-app:test

After the application starts, test communication by container name:

    docker run --rm --name network-test --network app-net curlimages/curl:8.5.0 http://app-test:8000

The network-test container is automatically removed after the request.

Clean up:

    docker stop app-test
    docker rm app-test
    docker network rm app-net
