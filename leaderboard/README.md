# Go Redis REST API Example

This is a simple example of a REST API built with Go that simulates a game leaderboard using Redis as a data store. Users can add themselves to the game, play the game, and view the leaderboard.

## Prerequisites

- Go installed on your machine. Installation instructions can be found [here](https://golang.org/doc/install).
- Docker or Podman installed on your machine. Installation instructions for Docker can be found [here](https://docs.docker.com/get-docker/) and for Podman [here](https://podman.io/getting-started/installation).

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/golang-redis-leaderboard.git
cd golang-redis-leaderboard
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

### Register a User

Note: For your convenience, the application automatically registers ten users (user-1 through user-10) at startup. This makes testing easier.

To register a new user, send a `POST` request with JSON payload to `/`:
``` bash
curl -i -XPOST -d 'user-11' localhost:8080
```

### Play

To simulate playing the game, send a `GET` request to `/play`.

```bash
curl http://localhost:8080/play
```

## View Leaderboard

To view the leaderboard, send a `GET` request to `/top/{n}`, where {n} is the number of top players you want to retrieve.

```bash
curl http://localhost:8080/top/5
```
