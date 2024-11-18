# Symfony Docker Environment

A Docker environment for Symfony framework, similar to Laradock, but tailored specifically for Symfony.

## Getting Started

### 1. Clone this repository anywhere on your machine:

```
git clone https://github.com/jobayer-mojumder/symdock.git
```

Your folder structure should look like this:

```
* symdock
* your-project
```

### 2. To use this environment, follow these steps:

Configure Environment Variables

##### Update the env file with your workplace location:

```
WORKPLACE_DIR=../your-project
```

#####  also update NGINX_SYMFONY_SERVER_NAME value in .env file

```
NGINX_SYMFONY_SERVER_NAME=symfony.localhost
```

### 3. Add the domains to the hosts files.

```
127.0.0.1  symfony.localhost
```

### 4. Build and Up Docker Containers
Run the following commands to build and start the Docker containers:

```
docker-compose build
docker-compose up -d
```

This will build the Docker images and start the containers in detached mode.

### 5. Access Your Symfony Project
Your Symfony project should now be accessible at http://symfony.localhost (or the port you specified in the docker-compose.yml file).

## Features

This environment includes the following services:

PHP 8.3

MySQL 8.0

Nginx

## Configuration

You can customize the environment by modifying the docker-compose.yml file and the env file.

## Contributing

Contributions are welcome! If you'd like to add a new service or improve an existing one, please submit a pull request.

## License

This project is licensed under the MIT License.
