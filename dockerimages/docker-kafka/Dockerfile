# Kafka

FROM openjdk:8-jdk
WORKDIR /main

RUN apt-get update && \
	apt-get upgrade -y && \
	apt install -y nano python3

# Kafka
RUN wget https://archive.apache.org/dist/kafka/2.3.0/kafka_2.12-2.3.0.tgz && \
	tar -xzf kafka_2.12-2.3.0.tgz && \
	rm kafka_2.12-2.3.0.tgz

# Zookeeper
RUN wget https://archive.apache.org/dist/zookeeper/zookeeper-3.5.5/apache-zookeeper-3.5.5-bin.tar.gz && \
	tar -xvzf apache-zookeeper-3.5.5-bin.tar.gz && \
	rm apache-zookeeper-3.5.5-bin.tar.gz

# our repo with data and models trained
RUN apt-get install git -y && \
	git clone https://github.com/irenegl3/practica_big_data_2020-v2 && \
	mv practica_big_data_2020-v2/* . && \
	rm -r practica_big_data_2020-v2

RUN chmod +x scripts/startkafkaserver.sh

WORKDIR /main/kafka_2.12-2.3.0
CMD ./../scripts/startkafkaserver.sh
#CMD ["sleep", "123456"]
