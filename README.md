```sh
######################################################
#  ____             _             _   _ _   _ _      #
# |  _ \  ___   ___| | _____ _ __| | | | |_(_) |___  #
# | | | |/ _ \ / __| |/ / _ \ '__| | | | __| | / __| #
# | |_| | (_) | (__|   <  __/ |  | |_| | |_| | \__ \ #
# |____/ \___/ \___|_|\_\___|_|   \___/ \__|_|_|___/ #
#                                                    #
######################################################
```
# Pre-requisites:
* Install [docker]
* Install [docker compose]

# Setup
* Clone or download this repository.
    ```sh
    $ git clone https://github.com/Nanielito/DockerUtils.git
    ```
* Run the install script to put binary and example files into your docker compose configuration directory:
    ```sh
    $ ./install -d DOCKER_COMPOSE_CONFIGURATION_DIRECTORY
    ```
* Go to your docker compose configuration directory
* Run the script template generator to create all scripts you need to handle docker and docker compose commands (*):
    ```sh
    $ bin/generator -n EXECUTABLE_NAME -d EXECUTABLE_DIRECTORY -t TEMPLATE_TYPE
    ```
##### (*) Notes:
* `EXECUTABLE_NAME must be defined as a service in your docker-compose.yml file.`
* `EXECUTABLE_DIRECTORY must be a directory path inside your docker compose configuration directory.`
* `TEMPLATE_TYPE must be 'specific' (default value) or 'generic'.`
  
# Examples
If there is a service named app in your docker-compose.yml file, you can create a script for app:
```sh
$ bin/generator -n app -d myapp
```
This will create a directory named 'myapp' into your docker compose configuration directory and a script named 'app'
inside it. Then, you can call regular docker commands as follows (*):
```sh
$ bin/app pull
$ bin/app up
$ bin/app start
$ bin/app restart
$ bin/app stop
$ bin/app rm
$ bin/app clean
$ bin/app exec COMMAND [ARGS]
$ bin/app logs
$ bin/app ps
$ bin/app set FILE CONTAINER_DIRECTORY
$ bin/app get CONTAINER_FILE DIRECTORY
```
##### (*) Notes:
`Previous commands run over the 'app' service defined in your docker-compose.yml file.`

# Script Types
You can generate the following script types:
* **Specific script**: A script which handles docker commands over a simple specific service.
* **Generic script**: A script which handles docker commands over multiple services.

A specific script can be created following the steps shown in the [example section](#examples). Alternatively, you can
pass the `-t specific` flag value to  create it:
```sh
$ bin/generator -n app -d myapp -t specific
```
A generic script can be created running the following command:
```sh
$ bin/generator -n app -d myapp -t generic
```
Then, you can call regular docker commands as follows:
```sh
$ bin/app pull    [CONTAINER_NAME|...]
$ bin/app up      [CONTAINER_NAME|...]
$ bin/app start   [CONTAINER_NAME|...]
$ bin/app restart [CONTAINER_NAME|...]
$ bin/app stop    [CONTAINER_NAME|...]
$ bin/app rm      [CONTAINER_NAME|...]
$ bin/app clean   [CONTAINER_NAME|...]
$ bin/app exec    CONTAINER_NAME COMMAND [ARGS]
$ bin/app logs    [CONTAINER_NAME|...]
$ bin/app ps      [CONTAINER_NAME]
$ bin/app set     CONTAINER_NAME FILE CONTAINER_DIRECTORY
$ bin/app get     CONTAINER_NAME CONTAINER_FILE DIRECTORY
```

# Commands
* **pull**: Pulls the docker image related to a service defined in your docker-compose.yml file.
* **up**: Creates and runs the container related to a docker image (in detach mode).
* **start**: Starts a container.
* **restart**: Restarts a container.
* **stop**: Stops a container.
* **rm**: Removes a container.
* **clean**: Stops and removes a container.
* **exec**: Executes a container command.
* **logs**: Displays the log file related to a container.
* **ps**: Displays the process status related to a container.
* **set**: Copies a local file to a container using docker cp.
* **get**: Retrieves a file from a container using docker cp.

[//]: # (Reference links)
[docker]: <https://docs.docker.com/engine/installation/#server>
[docker compose]: <https://docs.docker.com/compose/install/>
