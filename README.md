# Server-Manager-Docker-Compose
## Steps For Executing Docker Compose

1. #### Build Docker Image :-
```bash
   $ docker build -t restapi11 .
```
2. #### Compose Up :-
```bash
   $ docker compose up
```

## docker-compose.yml :

```yml
  version : '3'
services:

  database:
    image: 'mongo'
    container_name: 'mongo_container'
    volumes:
      - mongodb_data:/data/db
    environment:
      - MONGO_INITDB_DATABASE=server_db
      - MONGO_INITDB_ROOT_USERNAME=aman
      - MONGO_INITDB_ROOT_PASSWORD=aman
    ports:
    - 27017:27017

  restapi:
    image: 'restapi11'
    container_name: 'restapi_container'
    ports:
    - 8080:8080
    links:
    - database

volumes:
  mongodb_data:
    driver: local
```

## Docker File REST-API
```yml
  #Pull base image
  FROM tomcat:8.5.30-jre8

  # Maintainer
  MAINTAINER "aman.saxena2898@gmail.com"

  COPY "restapi.war" "/usr/local/tomcat/webapps/restapi.war"

  EXPOSE 8080

  CMD ["catalina.sh", "run"]

```
