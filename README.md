# KafkaRaftDocker
Apache Kafka cluster with Raft

# TEST PRODUCER/CONSUMER

## ON HOST MACHINE
### Create Topic
./kafka-topics.sh --create --topic topic1 --partitions 3 --replication-factor 3 --bootstrap-server localhost:9094

### Producer
./kafka-console-producer.sh --bootstrap-server localhost:9094  --topic test

### Consumer
./kafka-console-consumer.sh --bootstrap-server localhost:9094  --topic test --from-beginning


## INSIDE DOCKER CONTAINER
### Create Topic
docker-compose exec kafka-0 /opt/bitnami/kafka/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test

### Producer
docker-compose exec kafka-0 /opt/bitnami/kafka/bin/kafka-console-producer.sh --bootstrap-server kafka-0:9092 --producer.config /opt/bitnami/kafka/config/producer.properties --topic test

### Consumer
docker-compose exec kafka-0 /opt/bitnami/kafka/bin/kafka-console-consumer.sh --bootstrap-server kafka-0:9092 --consumer.config /opt/bitnami/kafka/config/consumer.properties --topic test --from-beginning

### Permissions
sudo mkdir -p /opt/kafka/volumes/kafka0
sudo mkdir -p /opt/kafka/volumes/kafka1
sudo mkdir -p /opt/kafka/volumes/kafka2

## grant all write
sudo chmod -R a+w /opt/kafka
## Or grant just the bitnami/kafka container user id (UID)
sudo chown -R 1001:1001
sudo chmod -R ug+rw /opt/kafka

Resources:
https://docs.bitnami.com/google-templates/infrastructure/kafka/administration/run-producer-consumer/