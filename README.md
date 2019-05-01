# spring-boot-docker-mysql
Spring Boot test application running inside docker container linked with MySQL container.

## How to run it with Docker
Assume you already have Docker installed. See https://docs.docker.com/installation/.

First, clone the project and build locally:

~~~
git clone https://github.com/jiwhiz/spring-boot-docker-mysql.git
cd spring-boot-docker-mysql
mvn clean package docker:build
~~~

Run MySQL 5.6 in Docker container:

~~~
docker run --name mysql-test -e MYSQL_ROOT_PASSWORD=root#123 -e MYSQL_DATABASE=test -e MYSQL_USER=test -e MYSQL_PASSWORD=test926 -d mysql:5.6
~~~

Check the log to make sure the server is running OK:
~~~
docker logs mysql-test
~~~

Run test application in Docker container and link to mysql-test:

~~~
docker run -p 8080:8080 --name test-app --link mysql-test:mysql -d saurav/spring-boot-docker-mysql
~~~

You can check the log by
~~~
docker logs test-app
~~~

Open http://localhost:8080 in browser and you should see the message.

