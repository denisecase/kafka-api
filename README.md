# kafka-api

Explore super-fast Apache Kafka.

- [Quick Start](https://kafka.apache.org/quickstart). 
- [Tutorial](https://kafka.apache.org/31/documentation/streams/tutorial)

## Recommended Tools

* [VS Code](https://code.visualstudio.com/)
* [VS Code Extension - Java Extension Pack](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)
* [Context Menu: Add Open PowerShell Here as Administrator](https://www.tenforums.com/tutorials/60177-add-open-powershell-window-here-administrator-windows-10-a.html)

## Prerequisities

* OpenJDK or JDK (8 or up)

-----

## 1. Install Apache Kafka

  - Go to Apache Kafka Downloads
  - Download kafka_2.13-3.1.0.tgz (~84 MB)
  - Extract it: Open Git Bash and run `tar -xzf kafka_2.13-3.1.0.tgz`
  - Move the folder to C:\

## 2. Configure Apache Kafka

* Configure Kafka (change 2 lines):
  - In C:\kafka_2.13-3.1.0/config/zookeeper.properties, set:
  - `dataDir=C:/kafka_2.13-3.1.0/zookeeper-data`
  - In C:\kafka_2.13-3.1.0/config/server.properties, set:
  - `log.dirs=C:/kafka_2.13-3.1.0/kafka-logs`

-----
  
## 3. Start Zookeeper Service (PS Process 1 - keep open, minimize)

`C:\kafka_2.13-3.1.0\bin\windows\zookeeper-server-start.bat C:\kafka_2.13-3.1.0\config\zookeeper.properties`

## 4. Start Kafka Service (PS Process 2 - keep open, minimize)

`C:\kafka_2.13-3.1.0\bin\windows\kafka-server-start.bat C:\kafka_2.13-3.1.0\config\server.properties`

-----

## 5. Create a Kakfa Topic (PS Process 3 - keep open, producer)

Create a Topic to Store Events:

`C:\kafka_2.13-3.1.0\bin\windows\kafka-topics.bat --create --topic quickstart-events --bootstrap-server localhost:9092`

Write some events to the topic:

`C:\kafka_2.13-3.1.0\bin\windows\kafka-console-producer.bat --topic quickstart-events --bootstrap-server localhost:9092`


## 6. Read from a Kakfa Topic (PS Process 4 - keep open, consumer)

Read the events:

`C:\kafka_2.13-3.1.0\bin\windows\kafka-console-consumer.bat --topic quickstart-events --from-beginning --bootstrap-server localhost:9092`

-----

## Run Streams Example

Open PowerShell as Administrator in the root project folder, compile the code using Maven and create an executable jar file. Generated artifacts can be found in the new 'target' folder.

```PowerShell
mvn clean package
mvn exec:java -D exec.mainClass=myapps.Pipe
```

## Create Topics and Rerun (Three New PS Process Windows)

Create input topic:

`C:\kafka_2.13-3.1.0\bin\windows\kafka-topics.bat --create --topic streams-plaintext-input --bootstrap-server localhost:9092`

Write some events to the input topic:

`C:\kafka_2.13-3.1.0\bin\windows\kafka-console-producer.bat --topic streams-plaintext-input --bootstrap-server localhost:9092`

Read from pipe output topic:

`C:\kafka_2.13-3.1.0\bin\windows\kafka-console-consumer.bat --topic streams-pipe-output --from-beginning --bootstrap-server localhost:9092`

Send content to input topic:

`type file-input.txt | C:\kafka_2.13-3.1.0\bin\windows\kafka-console-producer.bat --topic streams-plaintext-input --bootstrap-server localhost:9092`

Read from wordcount output topic:

`C:\kafka_2.13-3.1.0\bin\windows\kafka-console-consumer.bat --topic streams-wordcount-output --from-beginning --bootstrap-server localhost:9092`

Read from linesplit output topic:

`C:\kafka_2.13-3.1.0\bin\windows\kafka-console-consumer.bat --topic streams-linesplit-output --from-beginning --bootstrap-server localhost:9092`

## Explore

Get information about the topic.

`C:\kafka_2.13-3.1.0\bin\windows\kafka-topics.bat --topic quickstart-events --bootstrap-server localhost:9092 --describe`

## Resources

- <https://docs.confluent.io/4.1.1/streams/quickstart.html>

## Repository

- Source: https://github.com/denisecase/kafka-api

## Collaborators

- Denise Case

