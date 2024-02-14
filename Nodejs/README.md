# Getting started

This repository is a sample application for users following the getting started guide at https://docs.docker.com/get-started/.

The application is based on the application from the getting started tutorial at https://github.com/docker/getting-started


## To normally start container

docker run -d -p 3000:3000                                  \
        --name test                                         \
        --mount type=volume,src=todo-bd,target=/etc/todos   \
        node-app

## To run the application in Development mode:
docker run -d -p 3000:3000                                                      \
        --name test                                                             \
        --mount type=volume,src=todo-bd,target=/etc/todos                       \
        -w /app                                                                 \
        --mount type=bind,src="E:\Docker\Repo\getting-started-app",target=/app  \
        node-app sh -c "yarn install && yarn run dev"

## To start MySQL database as container
docker run -d                                       \
        --network todo-app --network-alias mysql    \
        -v todo-mysql-data:/var/lib/mysql           \
        -e MYSQL_ROOT_PASSWORD=secret               \
        -e MYSQL_DATABASE=todos                     \
        mysql:8.0

## To run the application in Development mode with sql env values:
docker run -dp 127.0.0.1:3000:3000 \
  -w /app -v "E:\Docker\Repo\getting-started-app:/app" \
  --network todo-app \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=secret \
  -e MYSQL_DB=todos \
  node:18-alpine \
  sh -c "yarn install && yarn run dev"

docker run -dp 127.0.0.1:3000:3000 -w /app -v "E:\Docker\Repo\getting-started-app:/app" --network todo-app -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=secret -e MYSQL_DB=todos node:18-alpine sh -c "yarn install && yarn run dev"