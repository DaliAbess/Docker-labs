# Lab #2: Docker Compose Help Command
## Overview
The `docker-compose` help command is used to list out all the subcommands that can be used with `docker-compose`. This lab will cover the usage of the `docker-compose help` command and its various options.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To get started with the `docker-compose help` command, follow these steps:
1. Open a terminal in your Alpine OS instance.
2. Run the command `docker-compose help` to list out all the subcommands that can be used with `docker-compose`.
3. You can also try `--help` or `-h` instead of `help`.

### Checking Docker Compose Help Command
```bash
$ docker-compose help
```
This command will display the usage and options for `docker-compose`.

## Usage and Options
The `docker-compose help` command displays the following usage and options:
```
Define and run multi-container applications with Docker.
Usage:
  docker-compose [-f <arg>...] [options] [COMMAND] [ARGS...]
  docker-compose -h|--help

Options:
  -f, --file FILE             Specify an alternate compose file (default: docker-compose.yml)
  -p, --project-name NAME     Specify an alternate project name (default: directory name)
  --verbose                    Show more output
  --log-level LEVEL            Set log level (DEBUG, INFO, WARNING, ERROR, CRITICAL)
  --no-ansi                    Do not print ANSI control characters
  -v, --version                Print version and exit
  -H, --host HOST              Daemon socket to connect to
  --tls                        Use TLS; implied by --tlsverify
  --tlscacert CA_PATH          Trust certs signed only by this CA
  --tlscert CLIENT_CERT_PATH   Path to TLS certificate file
  --tlskey TLS_KEY_PATH        Path to TLS key file
  --tlsverify                  Use TLS and verify the remote
  --skip-hostname-check        Don't check the daemon's hostname against the name specified in the client certificate
  --project-directory PATH    Specify an alternate working directory (default: the path of the Compose file)
  --compatibility              If set, Compose will attempt to convert deploy keys in v3 files to their non-Swarm equivalent
```

## Commands
The `docker-compose help` command lists out the following commands:
* `build`: Build or rebuild services
* `bundle`: Generate a Docker bundle from the Compose file
* `config`: Validate and view the Compose file
* `create`: Create services
* `down`: Stop and remove containers, networks, images, and volumes
* `events`: Receive real time events from containers
* `exec`: Execute a command in a running container
* `help`: Get help on a command
* `images`: List images
* `kill`: Kill containers
* `logs`: View output from containers
* `pause`: Pause services
* `port`: Print the public port for a port binding
* `ps`: List containers
* `pull`: Pull service images
* `push`: Push service images
* `restart`: Restart services
* `rm`: Remove stopped containers
* `run`: Run a one-off command
* `scale`: Set number of containers for a service
* `start`: Start services
* `stop`: Stop services
* `top`: Display the running processes
* `unpause`: Unpause services
* `up`: Create and start containers
* `version`: Show the Docker-Compose version information

## Trying Help Commands for Subcommands
You can also try help for `docker-compose` subcommands. For example:
```bash
$ docker-compose build --help
```
This command will display the usage and options for the `build` subcommand.

### Build Subcommand
The `build` subcommand is used to build or rebuild services. The usage and options for the `build` subcommand are:
```
Build or rebuild services.
Services are built once and then tagged as `project_service`,
e.g. `composetest_db`. If you change a service's `Dockerfile` or the
contents of its build directory, you can run `docker-compose build` to rebuild it.
Usage: build [options] [--build-arg key=val...] [SERVICE...]
Options:
  --compress              Compress the build context using gzip.
  --force-rm               Always remove intermediate containers.
  --no-cache               Do not use cache when building the image.
  --pull                   Always attempt to pull a newer version of the image.
  -m, --memory MEM         Sets memory limit for the build container.
  --build-arg key=val       Set build-time variables for services.
  --parallel               Build images in parallel.
```

## Expected Output
The expected output of the `docker-compose help` command is a list of all the subcommands that can be used with `docker-compose`, along with their usage and options.

## Key Concepts
The key concepts covered in this lab are:
* The `docker-compose help` command and its usage
* The various options available with the `docker-compose` command
* The subcommands available with `docker-compose`, such as `build`, `bundle`, `config`, etc.
* The usage and options for each subcommand, such as the `build` subcommand.

---


