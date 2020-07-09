## Laravel 7 files with docker containerisation

- the laravel application is set in the ```src``` folder
- the ```nginx``` folder and the ```mysql``` folder are configuration folders as defined in the ```docker-compose.yml``` file
- To build these containers and run, from the terminal, run  ```docker-compose build && docker-compose up -d ```
- ```-d``` stands for detach that enables our container to run in the background until it is brought down
- Or you can run ```docker-compose up -d --build```
- to execute artisan commands, run ```docker-compose exec php php /var/www/html/artisan migrate```
- where, ```php``` stands for the service name in the php container and ```php /var/www/html/artisan migrate``` is the ```php artisan migrate``` command
- <b>Note:</b> Dont forget to update database connection settings in the ```.env``` file in the laravel directory to the mysql service name

<pre><code>
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
</code></pre>

- To power down our containers, ```docker-compose down```

## Using composer
- To view composer docker service, check ```docker-compose.yml``` file
- In the root directory, to bring up the composer container and then down after the task is completed, run ```docker-compose run --rm composer require package_name``` 
- ```rm``` flag tells docker to bring down the container when task is complete
- To execute composer commands on build, define the run commands in the ```Dockerfile```
- i.e. add ```RUN composer install``` to the Dockerfile

## Using npm
- To run node or npm commands without installing them locally, use the npm service in the ```docker-compose.yml``` file
- in the root directory run ```docker-compose run --rm npm install``` to download the necessary dependencies
- To package npm with laravel's webpack mix, run ```docker-compose run --rm npm run dev``` to get compiled assets
- Just like composer, to run npm commands on building the docker containers, define the commands in the ```Dockerfile```.
- i.e. add ```RUN npm install``` and ```RUN npm run build``` to the Dockerfile

## Using artisan
- Inorder to run the artisan commands from the root directory, need to add an artisan service and container
- with the ```artisan``` serve, you can run ```docker-compose run --rm artisan migrate``` instead of the legacy way of running ```docker-compose exec php php /var/www/html/artisan migrate``` 
- <b>Note</b>Make sure the mysql connection settings in the ```.env``` file are set properly as defined above.
