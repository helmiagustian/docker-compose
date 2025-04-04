# Makefile for Kafka testing

KAFKA_CONTAINER_NAME=kafka
KAFKA_BROKER=localhost:9092
TOPIC=test-topic
GROUP=test-group
JSON_FILE=message.json  # Change this to the actual JSON file path

.PHONY: help start stop logs create-topic list-topics produce consume consume-group

help:
	@echo "Kafka Makefile Commands:"
	@echo "  make start           - Start Kafka using docker-compose"
	@echo "  make stop            - Stop Kafka"
	@echo "  make logs            - Show Kafka logs"
	@echo "  make create-topic    - Create a test topic"
	@echo "  make list-topics     - List all topics"
	@echo "  make produce         - Produce messages to a topic"
	@echo "  make consume         - Consume messages from a topic"
	@echo "  make consume-group   - Consume messages with a group ID"

start:
	docker-compose up -d

stop:
	docker-compose down

logs:
	docker logs -f $(KAFKA_CONTAINER_NAME)

create-topic:
	docker exec -it $(KAFKA_CONTAINER_NAME) \
	kafka-topics --create --topic $(TOPIC) --bootstrap-server $(KAFKA_BROKER) --partitions 1 --replication-factor 1

list-topics:
	docker exec -it $(KAFKA_CONTAINER_NAME) \
	kafka-topics --list --bootstrap-server $(KAFKA_BROKER)

produce:
	docker exec -it $(KAFKA_CONTAINER_NAME) \
	kafka-console-producer --broker-list $(KAFKA_BROKER) --topic $(TOPIC)

produce-json:
	cat $(JSON_FILE) | docker exec -i $(KAFKA_CONTAINER_NAME) \
	kafka-console-producer --broker-list $(KAFKA_BROKER) --topic $(TOPIC)

consume:
	docker exec -it $(KAFKA_CONTAINER_NAME) \
	kafka-console-consumer --bootstrap-server $(KAFKA_BROKER) --topic $(TOPIC) --from-beginning

consume-group:
	docker exec -it $(KAFKA_CONTAINER_NAME) \
	kafka-console-consumer --bootstrap-server $(KAFKA_BROKER) --topic $(TOPIC) --group $(GROUP) --from-beginning
