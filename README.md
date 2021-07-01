# laravel-docker
Instalation and configuration Laravel + php7.4 + nginx + mysql in docker container

1 - Clone github's laravel repository to a directory by calling laravel-app and access laravel-app directory

```
git clone https://github.com/laravel/laravel.git laravel-app && cd laravel-app
```

2 - Install project dependencies using a composer docker image

```
docker run --rm -v $(pwd):/app composer install
```

>Using the -v and --rm flags with docker run creates an ephemeral container that will be mounted and linked to your current directory before being removed

3 - Set permissions on the project directory to your non-root user

```
sudo chown -R $USER: ./
```

4 - Clone github's laravel-docker repository to a directory by calling docker, move the files to the project folder and remove the empty docker directory

```
git clone https://github.com/utilcodebr/laravel-docker.git docker && mv docker/* . && rm -rf docker/
```

5 - Create .env file and set MySQL database connection settings according to docker-composer.yml file

```
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=secret
```

6 - Start all containers, create volumes, and configure and connect networks

```
docker-compose up -d
```

>The -d flag makes the process daemon, running its containers in the background.

7 - The artisan commands now work via docker-compose exec app

```
docker-compose exec app php artisan key:generate
```

>The "app" parameter refers to the name of the container in which laravel is running

8 - Stop all application containers
```
docker-compose down
```

>Remember: docker-compose commands will only work in the project directory.

>If you use a windows operating system, I recommend using the [gitbash software](https://git-scm.com/downloads) to introduce the described bash commands
