# KafkaRaftDocker
Apache Kafka cluster with Raft


### Test Commands 

# Export Auth ENV Variable
export KAFKA_OPTS="-Djava.security.auth.login.config=/opt/bitnami/kafka/config/kafka_jaas.conf"

# Create Topic
/opt/bitnami/kafka/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test


# Producer
/opt/bitnami/kafka/bin/kafka-console-producer.sh --bootstrap-server kafka-0:9092 --producer.config /opt/bitnami/kafka/config/producer.properties --topic test

# Consumer
/opt/bitnami/kafka/bin/kafka-console-consumer.sh --bootstrap-server kafka-0:9092 --consumer.config /opt/bitnami/kafka/config/consumer.properties --topic test --from-beginning
