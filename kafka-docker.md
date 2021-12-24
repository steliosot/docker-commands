# Install docker compose

## Get the library
    $ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

## Change permissions

    $ sudo chmod +x /usr/local/bin/docker-compose

## Check that docker-compose is installed

    $ docker-compose --version

# Install Kafka on docker

## Create a new folder and enter

    $ mkdir kafka-installation
    $ cd kafka-installation/


## Create a new docker-compose.yml file

    version: '3'

    services:
    zookeeper: 
        image: wurstmeister/zookeeper
        container_name: zookeeper
        ports:
        - "2181:2181"

    kafka:
        image: wurstmeister/kafka
        container_name: kafka
        ports:
        - "9092:9092"
        environment:
        KAFKA_ADVERTISED_HOST_NAME: localhost
        KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181

## Run the docker-compose file

    $ docker-compose -f docker-compose.yml up -d

## If you want to stop it (dont stop it)

    $ docker-compose -f docker-compose.yml down -d

## Enter in the container

    $ docker exec -it kafka /bin/sh

## Create a new topic

    $ ./opt/kafka/bin/kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 1 --topic student-topic

## List available topics

    $ ./opt/kafka/bin/kafka-topics.sh --list --zookeeper zookeeper:2181

# Create a python Consumer-Producerr scripts to connect

## Create a consumer
> kafka-consumer.py

```python
from kafka import KafkaConsumer
consumer = KafkaConsumer('student-topic')
for message in consumer:
    print (message)
```

## Create a producer

> kafka-producer.py

> * Make sure you update the server IP!

```python
from kafka import KafkaProducer
producer = KafkaProducer(bootstrap_servers='104.154.204.151:9092')
producer.send('student-topic', b'Hello, World!')
producer.send('student-topic', key=b'message-two', value=b'This is Kafka message from the producer')
producer.flush()
```
