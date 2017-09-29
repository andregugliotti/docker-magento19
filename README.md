# Magento 1.9 Docker Container

This Docker container is build with support to `Nginx`, `PHP 5.6` (built with PHP FPM) and `MySQL 5.7`. It is also shipped with `PHPMyAdmin` and `xDebug`. Additionally, you can enable support for ionCube Loader, uncommenting the right lines at _docker-magento19/php/Dockerfile_.
It contains a Magento 1.9.3.4 CE installation, with sample data.

## How to use this repository

Just clone the files into your project folder. It is a raw Docker container with no frameworks or files, to be used as start point to your project.

There are three folders:

- docker-magento19 - that is the folder for Docker files
- htdocs - that is the root folder, where website files are copied (I recommend the use of an automatic deploy, probably included in your IDE). Magento source files are here
- project - that is the project folder, where you should work

### Starting the container

Just open your terminal and navigate to docker-magento19 of this project. Type:

`docker-compose up -d`

Docker will build the containers and start them. You must also map the address _127.0.0.1 m1.docker.dev_ on your hosts file. If you don't know how to do that, just google it. It's easy!

### Importing Magento DB

On this project you find a base DB, on folder sample-db. To use it, you just import it over magento1 DB, using PHPMyAdmin or your favourite MySQL client.
If you prefer not use sample data, just comment this line on _docker-compose-yml_, _project_ node, rebuild your containers and proceed to a regular install of Magento.

`- local.xml:/var/www/htdocs/etc/local.xml`

### Changing project / htdocs files

To see your site live, just open a browser and visit m1.docker.dev. That's exactly what you find at folder htdocs and it's automatically updated when you change them on your local machine. So, you don't need to rebuild your container to see your files.
Don't forget that the live folder is htdocs. Project folder is only local.

### Accessing Magento backend

When using sample data, just navigate to m1.docker.dev/admin and access the panel with these credentials:

username: `admin`
password: `a123456`
 
### Seeing logs

All logs are saved locally, on folder docker-magento19/logs. You can control them on your local machine.
Access logs are disabled from nginx config files. If you need them, see docker-magento19/nginx conf files.

### Accessing the container terminal

If you need to access the container terminal, use the following commands:

- to see which are the running containers: `docker ps`
- to connect to a container as root: `docker exec -it {container_name} bash`
- to connect to a container as local user (1000): `docker exec -it --user local {container_name} bash`

This last option is useful when you need to connect to the container and run an non root user (like when you need to run a console script).

### Adding a database

Database files are found on docker-magento19/databases and use a specific user, which means no access from the local machine. They are not included on git repository.
If you have some problems starting the MySQL container, try to empty this folder and build the container again.

### Connecting to DB

To create a DB and set user credentials, check docker-magento19/docker-compose.yml file. You find the entries at mysql node.

To connect to a DB from local machine, just use the localhost address (like 127.0.0.1) and the credentials.

To connect to a DB from another container, like from a framework running on php side, use the entry `mysql` as address/server

### Using PHPMyAdmin

This project is shipped with a PHPMyAdmin instance. It is accessible via 8084 port. So, just navigate to `project1.docker.dev:8084` and use same credentials informed at docker-compose.yml file.

## Contribution

This is an open source module and can be used as a base for other modules. If you have suggestions for improvements, just submit your pull request.

## Versioning

We use SemVer to versioning. To view all versions for this module, visit the tags page, on this repository.

## Authors

Andre Gugliotti - Initial module development - [AndreGugliotti](https://github.com/AndreGugliotti)
See also the developers list, with all those who contributed to this project. [Contributors](https://github.com/andregugliotti/docker-magento19/graphs/contributors)

## License

This project is licensed under GNU General Public License, version 3.