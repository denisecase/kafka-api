# Challenge

Have the following installed and ready on your machine:

- OpenJDK (recommended) or Java JDK
- Maven (a popular Java build tool)]
- Zookeeper (configuration service for distributed systems)
- Kafka (streaming platform)

## Verify Installation

Test them by opening PowerShell anywhere and running:

```PowerShell
java -version
mvn -v
```

## Verify Configuration

Confirm that you have configured Zookeeper and Kafka correctly:

1. C:\apache-zookeeper-3.5.6-bin\conf\zoo.cfg with
2. dataDir=C:\apache-zookeeper-3.5.6-bin\data
3. C:\kafka_2.12-2.3.0\bin\windows\server-properties with
4. log.dirs=C:\kafka_2.12-2.3.0\logs

## Preparation: Start Zookeeper Service

Open PowerShell as Administrator from your desktop and run:

```PowerShell
zkServer
```

## Preparation: Start Kafka Service

Open PowerShell as Administrator from C:\kafka_2.12-2.3.0\bin\windows

```PowerShell
 .\kafka-server-start.bat .\server.properties
```

## Preparation: Create a Topic named test

Open PowerShell as Administrator from C:\kafka_2.12-2.3.0\bin\windows

```PowerShell
./kafka-topics.bat --zookeeper localhost:2181 --create  --replication-factor 1 --partitions 1 --topic test
```

## Preparation: Get the Code

Clone a fresh. copy of this repo https://github.com/denisecase/kafka-api. 

Mine is in C:\git\kafka-api.

## 1. Compile and Build Java Code

First, use Maven to clean, then compile, then create a fat jar with all dependencies. 

Open PowerShell as Administrator from this project folder.

```PowerShell
mvn clean compile assembly:single
```

## 2. Start Consumer

Open PowerShell as Administrator in the root project folder, start the original consumer app using topic test and group1 with:

```PowerShell
java -cp target/kafka-api-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.simple.Consumer test group1
```

## 3. Start One or More Producers

Open a new PowerShell as Administrator in the root project folder, start the Producer app using topic test:

```PowerShell
java -cp target/kafka-api-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.simple.Producer test
java -cp target/kafka-api-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.simple.ProducerHello test
java -cp target/kafka-api-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.simple.ProducerSentence test
java -cp target/kafka-api-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.simple.ProducerSentenceRandom test
```

## 4. Create a New Producer / Shutdown Ones

- Open the project folder in VS Code. 
- Create a new Producer. 
- Shut down any consumers or producers running. Why?
- Start over at step 1. 
- Repeat as desired.

## Questions

1. What is the path to your Zookeeper?  Does it have to be exactly C:\apache-zookeeper-3.5.6-bin? Why?
1. What is the path to your Kafka?  Does it have to be exactly C:\kafka_2.121.2.3.0? Why?
1. What is Zookeeper?
1. Why do we keep the Zookeeper Service PowerShell window open?
1. What is Kafka?
1. Why do we keep the Kafka Service PowerShell window open?
1. Where do we open PowerShell to run zkServer? Why?
1. Where do we open PowerShell to run Kafka commands? Why?
1. Where do we open PowerShell to run Maven commands? Why?
1. Do we open PowerShell as an Administrator? Or with regular privileges? Why?
1. What Kafka command are available to us?
1. What command do we use to start the service?
1. What command do we use to create a topic?
1. What is Maven?
1. What is the recommended Maven directory structure?
1. How do we run a Java executable class?
1. How do we know the Java class is executable?
1. How can we write information to the console in Java?
1. How do we create arrays in Java?
1. How can we generate random numbers in Java?
1. Why do we use namespaces in Java?
1. What do we have to change when put code in our own namepace in Java?
1. How many producers can we run at once?
1. How many consumers are we typically using?
1. What resources are useful for practicing Java coding skills?
