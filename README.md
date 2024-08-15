# HAWKI-Dockerfiles

An unofficial collection of various Dockerfiles for [HAWKI](https://github.com/HAWK-Digital-Environments/HAWKI).

## About

This repository serves the educational purpose of providing a starting point to building docker images for HAWKI and is **not affiliated with the HAWKI project**.  

The provided examples are mainly for running HAWKI locally, as they have **not been tested in a production environment**.

If your aim is to get HAWKI running in a local container as fast as possible, follow the instructions for the [PHP-Apache](#php-apache) image.

## Variants

### PHP-Apache

To try HAWKI in a local container, set the configuration variables following [the official documentation](https://github.com/HAWK-Digital-Environments/HAWKI?tab=readme-ov-file#configuration) in the `.env.example` file inside the `php-apache` folder. If you only want to inspect the running application without prompting any models, you don't have to configure anything. Simply login with the credentials for `TESTUSER` and `TESTPASSWORD` from the `.env.example` file.  
Run the container via `docker-compose` from the `php-apache` folder:

```bash
docker-compose up -d
```

HAWKI can then be reached from your localhost via [http://localhost:8080](http://localhost:8080).  

To stop the container, run:

```bash
docker-compose down
```

Alternatively, you can build and run the container without `docker-compose` from the `apache-php` folder with:

```bash
docker build . -t hawki-php-apache
docker run --name hawki-php-apache -p 8080:80 -d hawki-php-apache
```

If you wish to use your own configuration file, modify the command to include it as a mounted volume, replacing `PATH_TO_YOUR_CONFIG_FILE` with the path to your respective configuration file.

```bash
docker build . -t hawki-php-apache
docker run --name hawki-php-apache -p 8080:80 --mount type=bind,source=PATH_TO_YOUR_CONFIG_FILE,destination=/var/www/html/private/.env,readonly -d hawki-php-apache
```

To stop the container, run:

```bash
docker stop hawki-php-apache
```

To restart the container, run:

```bash
docker start hawki-php-apache
```

To remove the container, run:

```bash
docker rm hawki-php-apache
```
