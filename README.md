# Mosquitto MQTT Broker using docker compose

This is a simple [Mosquitto](https://mosquitto.org) broker to quickly initialize projects requiring an MQTT broker.

## Prerequisite

Before you can deploy Mosquitto using Docker Compose, you will need to have a few things in place. Here are the prerequisites:

- **Docker** - You will need to have [Docker](https://docs.docker.com/get-docker/) installed on your system. If you don't have Docker installed already, you can download it from the official Docker website. Be sure to download the version that is appropriate for your operating system.
- **Docker Compose** - You will also need to have Docker Compose installed on your system. Docker Compose comes pre-installed with Docker Desktop for Windows and macOS, but if you are using Linux or if you need to install it separately, you can follow the instructions on the [Docker Compose documentation page for Linux](https://docs.docker.com/compose/install/linux/).


## Configuration

The config file is in the file [mosquito.conf](./config/mosquitto.conf)

By default it's activated the log and data persistance (logs are in the `log` folder, and data are stored in a docker volume).


## Authentication

### Enable authentication

In the config file, set the value `allow_anonymous` to `false`, then uncomment the last line (`password_file`) and finaly restart the container.


### Change user password / create a new user

```bash
docker compose exec mosquitto mosquitto_passwd -b /mosquitto/config/password.txt user password
docker compose restart
```

### Delete user

```bash
docker compose exec mosquitto mosquitto_passwd -D /mosquitto/config/password.txt user
docker compose restart
```

## How to use

Clone this repo on your machine.

In a terminal window go to the folder where you cloned this repo. Default name is `mosquitto-compose`.

Then you can start Mosquitto:

```bash
docker compose up -d
```

Then Docker download mosquitto image and start the container.


```bash
PS C:\Projects\00-Docker-Projects\mosquitto-compose> docker compose up -d
[+] Running 4/4
 ✔ mosquitto Pulled                                                                                                4.1s
   ✔ 619be1103602 Pull complete                                                                                    1.2s
   ✔ 8432d2a45fb0 Pull complete                                                                                    1.4s
   ✔ 01fa0d8dc76f Pull complete                                                                                    1.5s
[+] Running 2/2
 ✔ Network mosquitto-compose_default  Created                                                                      0.2s
 ✔ Container mosquitto                Started                                                                      0.7s
PS C:\Projects\00-Docker-Projects\mosquitto-compose>
```

Now the Mosquitto broker is available at `localhost` port `1883`. 

You can test with a client like [MQTTX](https://mqttx.app/downloads).


## References

For creating this repo I used the following references:

- [How to setup Mosquitto MQTT Broker using docker](https://github.com/sukesh-ak/setup-mosquitto-with-docker)
- [Simple Mosquitto broker](https://github.com/vvatelot/mosquitto-docker-compose)

