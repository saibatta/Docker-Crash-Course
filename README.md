# Docker-Crash-Course

docker-compose.yaml 
==========================

```yaml
version: "3.8"
services: 
    nba-client:
        build:
            context: ./client
            dockerfile: dockerfile
        container_name: client-dc
        ports: 
            - 3000:3000
        volumes: 
            - './client:/usr/app'
            - '/usr/app/node_modules'
        environment: 
            - CHOKIDAR_USEPOLLING=true
    nba-server: #server name
        build: # build configuration
            context: ./server #Docker location 
            dockerfile: dockerfile # name of the Docker
        container_name: server-dc # Container name
        ports: #Port configuration (array of ports)
            - 5000:5000 #local machine port : docker continer port
        volumes: #volume configuration(array of volumes)
            - './server:/usr/app' #keep watching on the files changes
            - '/usr/app/node_modules' # don't touch the node_modules
        environment: 
            - CHOKIDAR_USEPOLLING=true #React application enviornment setup


```

- terminal from root directory of yaml file > **docker-compose up**  #build images and start running the container
- terminal from root directory of yaml file > **docker-compose down** # stop the container and remove it from the container

Build Docker image with dockerImage and tag as latest

	docker build -t dockerImage:latest .

export docker image

	docker save -o dockerImage_export.tar.gz dockerImage:latest

run the docker container with container name as dockerContainer and port 4502

	docker container run --name dockerContainer -p 4502:8080 dockerImage:latest

Stop a running container through SIGKILL(stop and remove the container)

	docker container kill dockerContainer

Delete an image from the local image store

	docker image rm dockerImage:latest



