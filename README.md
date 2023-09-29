# Docker + Apache + Php 8.2

<br />

## Links

http://127.0.0.1:80/ - Page (APACHE_80 in .env config)

http://127.0.0.1:80/phpinfo.php - Phpinfo


<br />

## Installation

1. Download the folder.

2. Create the file `./.docker/.env` by copying `./.docker/.env.example` and updating the `COMPOSE_PROJECT_NAME` and `port variables` if using multiple dockers.

3. Navigate to the `./docker` folder and run `docker-compose up -d --build` to start the containers.

4. To change apache root path `/var/www` to `/var/www/public`, edit the `./.docker/php/000-default.conf` file and update the `DocumentRoot`.

5. Now you can write PHP code in the `./app/www/public` folder.