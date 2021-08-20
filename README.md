# App and MongoDB with Docker-Compose
### docker-compose.yml
These kinds of files can create multiple services at the same time to further automate workloads. In this case it creates a single db instance using a Dockerfile and also a web instance from a previously made image with the environment variable already set.
```
services:
  # start the db image and map to port 27017
  db:
    build: ./db
    restart: always
    ports: [27017:27017]

  web:
    # start up the web app image and map to localhost
    image: salemsparta/eng89_multi-stage
    restart: always
    ports: [80:3000]
    # set variable for db port
    environment:
      - DB_HOST=mongodb://db:27017/posts
    # links the two images 
    depends_on:
      - db
```