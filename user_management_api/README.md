# Go Redis REST API Example

This is a simple example of a REST API built with Go that uses Redis as a data store. It allows users to create and retrieve user data via HTTP requests.

## Prerequisites

- Go installed on your machine. Installation instructions can be found [here](https://golang.org/doc/install).
- Docker or Podman installed on your machine. Installation instructions for Docker can be found [here](https://docs.docker.com/get-docker/) and for Podman [here](https://podman.io/getting-started/installation).

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/golang-redis-rest-api.git
cd golang-redis-rest-api
```

### 2. Pull the Redis Image
You need to have Redis running to use this application. You can pull the official Redis image from Docker Hub using Docker or Podman.

```bash
# Using Docker
docker pull redis

# Using Podman
podman pull docker.io/library/redis
```

### 3. Build and Run the Application

```bash
# Build the application
go build -o main .

# Run Redis container
docker run -d --name user-management-api -p 6379:6379 redis

# Run the application
./main
```

This will start the HTTP server on port 8080.

## Usage

Once the application is running, you can interact with it using HTTP requests.

### Create a User

To create a new user, send a `POST` request with JSON payload to `/`:
``` bash
curl -i -XPOST -d '{"email":"john@foo.com", "name":"john"}' localhost:8080/
curl -i -XPOST -d '{"email":"mary@foo.com", "name":"mary"}' localhost:8080/
```

### Retrieve a User

To retrieve a user by ID, send a GET request to `/{id}`:

```bash
curl http://localhost:8080/1
```

Replace 1 with the ID of the user you want to retrieve.

## Stopping the Application

To stop the application and clean up, press Ctrl + C to stop the server and remove the Redis container:

```bash
docker stop redis-server
docker rm redis-server
```
