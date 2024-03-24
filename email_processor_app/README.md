# Go Redis REST API Example

Sending emails is a common requirement for many websites. This is a perfect use case for leveraging background processing, because we don’t want the user or client to wait while the email is being sent. We’ll go over this a hypothetical solution based on the combination of a REST endpoint and a background job consumer implemented using a Redis list.

## Prerequisites

- Go installed on your machine. Installation instructions can be found [here](https://golang.org/doc/install).
- Docker or Podman installed on your machine. Installation instructions for Docker can be found [here](https://docs.docker.com/get-docker/) and for Podman [here](https://podman.io/getting-started/installation).

## Getting Started

### 1. Clone the Repository

```bash
git clone git@github.com:baconYao/golang-redis-playground.git
cd golang-redis-playground
```

### 2. Pull the Redis Image
You need to have Redis running to use this application. You can pull the official Redis image from Docker Hub using Docker or Podman.

```bash
# Using Docker
docker pull redis

# Using Podman
podman pull docker.io/library/redis

# Run Redis container
podman run -d --name email-processor -p 6379:6379 redis
```

### 3. Build and Run the Application

```bash
# Run the consumer application first
cd consumer
go run consumer.go

# Run the main application
go run main.go
```

This will start the HTTP server on port 8080.

## Usage

Once the application is running, you can interact with it using HTTP requests.

### Send Email Request

Once the Step 3 be done, open another terminal and to simulate email requests

``` bash
curl -i -XPOST -d '{"to":"baconyao@email.com","message":"Hi! How are you?"}' localhost:8080

#output
HTTP/1.1 200 OK
Jobid: 82
Date: Mon, 24 March 2022 14:32:51 GMT
Content-Length: 0

curl -i -XPOST -d '{"to":"judy@email.com","message":"Give me some money!!"}' localhost:8080

#output
HTTP/1.1 200 OK
Jobid: 888
Date: Mon, 24 March 2024 14:32:51 GMT
Content-Length: 0
```

### Checkb the Output of Consumer

You will see the similar output like below

```bash
received job 289
sending email Hi! How are you? to baconyao@email.com

received job 688
sending email Give me some money!! to judy@email.com
```
