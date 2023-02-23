# spring-boot-kafka-demo
Using Spring boot to demonstrate a simple producer / consumer messaging use case of Kafka. 

# Kafka setup

## Prerequisites
- `java 17`  (*Note: Kafka can run on `java 8+`, Since we plan to use `spring boot 3` `java 17` is required.*)

## Download
Download the latest Kafka release binary from the [official site](https://kafka.apache.org/downloads).

## Configure
[Official guide](https://kafka.apache.org/documentation/#quickstart) provides steps to quick start the Kafka environment in local.

### Windows
Users with Windows OS can follow the below step along with the official guide. 

- Create `c:\kafka` directory.
- Copy the `kafka*.tgz` file to `c:\kafka` directory.
- Extract the file in the `c:\kafka` location. This can be achieved in multiple ways. 
    - Using PowerShell `cd` into the kafka directory. 
    - `tar` command is available in PowerShell, using this the `*.tgz` file can be extracted. 
    - Run the command in PowerShell `tar -xvzf kafka_2.13-3.4.0.tgz` (Change the file name as per your download)
- After extracting the file, `cd` into the newly created `kafka_2.13-3.4.0` directory. 
- Two configuration files need to be changed. 
    - Change the `dataDir` value in `c:\kafka\kafka_2.13-3.4.0\config\zookeeper.properties` to `dataDir=c:/kafka/zookeeper-data`.
    - Change the `log.dirs` value in `c:\kafka\kafka_2.13-3.4.0\config\server.properties` to `log.dirs=c:/kafka/kafka-logs`

## Run
Follow the `Kafka with Zookeeper` section of the official guide. 

### Windows

Open windows command prompt. (Not PowerShell)
```
cd C:\kafka\kafka_2.13-3.4.0
```

```
.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
```

Keep this window running separately and open a new Command prompt.

```
cd C:\kafka\kafka_2.13-3.4.0
```
```
.\bin\windows\kafka-server-start.bat .\config\server.properties
```
Keep this window running separately. 

## Verify Installation
Your Kafka installation comes with utilities to test producer / consumer messaging. 

- Open windows command prompt
```
cd C:\kafka\kafka_2.13-3.4.0
```

### Create topic

```
.\bin\windows\kafka-topics.bat --create --topic quickstart-events --bootstrap-server localhost:9092
```

### Create message - Producer

```
.\bin\windows\kafka-console-producer.bat --topic quickstart-events --bootstrap-server localhost:9092
This is my first event
This is my second event
```

### Receive message - Consumer

```
.\bin\windows\kafka-console-consumer.bat --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
This is my first event
This is my second event
```

# Create Spring boot project
- Visit spring boot initializer site - https://start.spring.io

![springio.png](images/springio.png)

- As per above screenshot select the options and click generate to get the spring boot skeleton project.

- See the code in the repo for creating sample producer consumer messaging using Kafka.

# Run Spring boot project
- Spring boot project can be started using `mvn` as shown below.
```
mvn spring-boot:run
```
- Provide the message to the producer using the endpoint as shown below.
![send-to-topic.png](images/send-to-topic.png)

- As the message is received in the Consumer service, it is printed to console.
![received-message.png](images/received-message.png)

## Reference Documentation
For further reference, please consider the following sections:

* [Official Apache Maven documentation](https://maven.apache.org/guides/index.html)
* [Spring Boot Maven Plugin Reference Guide](https://docs.spring.io/spring-boot/docs/3.0.2/maven-plugin/reference/html/)
* [Create an OCI image](https://docs.spring.io/spring-boot/docs/3.0.2/maven-plugin/reference/html/#build-image)
* [Spring Web](https://docs.spring.io/spring-boot/docs/3.0.2/reference/htmlsingle/#web)
* [Spring for Apache Kafka](https://docs.spring.io/spring-boot/docs/3.0.2/reference/htmlsingle/#messaging.kafka)

## Guides
The following guides illustrate how to use some features concretely:

* [Building a RESTful Web Service](https://spring.io/guides/gs/rest-service/)
* [Serving Web Content with Spring MVC](https://spring.io/guides/gs/serving-web-content/)
* [Building REST services with Spring](https://spring.io/guides/tutorials/rest/)

