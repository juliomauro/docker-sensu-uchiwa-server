# docker-sensu-uchiwa-server

CentOS and sensu.
It runs sensu-api, sensu-server, redis, rabbitmq-server, uchiwa and ssh processes.

## Installation

Install from docker index or build from Dockerfile

## Docker pull

```
docker pull juliomauro/docker-sensu-uchiwa-server
```

or

## Git clone + docker build
```
git clone https://github.com/juliomauro/docker-sensu-uchiwa-server.git
cd docker-sensu-uchiwa-server
docker build -t yourname/docker-sensu-uchiwa-server .
```

## Run

```
docker run -d -p 10022:22 -p 3000:3000 -p 4567:4567 -p 5671:5671 -p 15672:15672 juliomauro/docker-sensu-uchiwa-server
```

## How to access via browser and sensu-client

### - rabbitmq console

* http://your-server:15672/
* id/pwd : sensu/password

###  - uchiwa

* http://your-server:3000/

###  - sensu-client

To run sensu-client, create client.json (see example below), then just run sensu-client process.

These are examples of sensu-client configuration.

* /etc/sensu/config.json

```
{
  "rabbitmq": {
    "host": "sensu-server-ipaddr",
    "port": 5671,
    "vhost": "/sensu",
    "user": "sensu",
    "password": "password",
    "ssl": {
      "cert_chain_file": "/etc/sensu/ssl/cert.pem",
      "private_key_file": "/etc/sensu/ssl/key.pem"
    }
  }
}
```

* /etc/sensu/conf.d/client.json

```
{
  "client": {
    "name": "sensu-client-node-hostname",
    "address": "sensu-client-node-ipaddr",
    "subscriptions": [
      "common",
      "web"
    ]
  },
  "keepalive": {
    "thresholds": {
      "critical": 60
    },
    "refresh": 300
  }
}
```

## ssh login

```
ssh mauro@localhost -p 10022
password: mauro
```

## License

MIT
