# Spark

FROM openjdk:8-jdk
WORKDIR /main

RUN apt-get update && \
	apt-get upgrade -y && \
	apt install -y nano python3 python3-pip

# sbt
RUN echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list && \
	curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | apt-key add && \
	apt-get update && \
	apt-get install sbt

# spark 2.4.4
RUN wget https://archive.apache.org/dist/spark/spark-2.4.4/spark-2.4.4-bin-hadoop2.7.tgz && \
	tar xzvf spark-2.4.4-bin-hadoop2.7.tgz && \
	rm spark-2.4.4-bin-hadoop2.7.tgz


# our repo with data and models trained
RUN apt-get install git -y && \
	git clone https://github.com/irenegl3/practica_big_data_2020-v2 && \
	mv practica_big_data_2020-v2/* . && \
	rm -r practica_big_data_2020-v2

# cargar models
RUN pip3 install -r requirements.txt

RUN chmod +x scripts/startspark.sh

WORKDIR /main
CMD ./scripts/startspark.sh
#CMD ["sleep", "123456"]
