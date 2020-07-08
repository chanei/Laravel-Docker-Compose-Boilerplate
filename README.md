### Laravel 7 files with docker containerisation

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

