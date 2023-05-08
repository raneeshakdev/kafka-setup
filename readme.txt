#To start the kafka on the local machine 
docker-compose up -d


#To create the topic 
docker-compose exec kafka kafka-topics.sh --create --topic test-topic --partitions 1 --replication-factor 1 --if-not-exists --zookeeper zookeeper:2181

docker-compose exec kafka bash -c "seq 100 | kafka-console-producer.sh --request-required-acks 1 --broker-list kafka:9092 --topic test-topic && echo 'Produced 100 messages.'"

#To consume the message from the kfaka
docker-compose exec kafka kafka-console-consumer.sh --bootstrap-server kafka:9092 --topic test-topic --from-beginning --max-messages 100
