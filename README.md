# kafka-api

Example Kafka Producer and Consumer apps.

Article: <https://www.javaworld.com/article/3060078/big-data/big-data-messaging-with-kafka-part-1.html>

Source: 

## Install Prerequisities

* 7-zip
* OpenJDK or JDK (8 or up)
* Maven
* Apache Zookeeper
* Kafka

Open PowerShell as Administrator and run:

```PowerShell
choco install 7zip -y
choco install openjdk -y
choco install maven -y
refreshenv
```

## Install Apache Zookeeper Binary Version

Go to <https://www.apache.org/dyn/closer.cgi/zookeeper/>. Choose site.  Chose the most current version (e.g., zookeeper-3.5.6), then download the file with "bin" in the name, e.g., apache-zookeeper-3.5.6-bin.tar.gz.

Extract and move to C:

1. Right-click the tar.gz file / 7-zip / extract here.
1. Right-click the .tar file / 7-zip / extract to the default apache-zookeeper folder (with version numbers).
1. When done, move the apache-zookeeper-3.5.6-bin folder to C:\.

## Install Kafka Binary Version

For Kafka, go to <https://kafka.apache.org/downloads>. Chose the most current binary version (e.g., 2.12), then download the tgz file, e.g.,  kafka_2.12-2.3.0.tgz.

Extract and move to C:

1. Right-click the tgz file / 7-zip / extract here.
1. Right-click the .tar file / 7-zip / extract to the default folder.
1. When done, move the kafka_2.12-2.2.0 folder to C:\.

## Set Zookeeper System Environment Variable

Windows + Edit System Environment Variables / Environment Variables / System Variables:

Variable name: ZOOKEEPER_HOME
Variable value: C:\apache-zookeeper-3.5.6-bin

## Verify Other Environment Variables

Your paths may be different - these are the ones on my machine:

JAVA_HOME   C:\Program Files\OpenJDK\jdk-13.0.1
KAFKA_HOME  C:\kafka_2.11-2.0.0
M2_HOME     C:\ProgramData\chocolatey\lib\maven\apache-maven-3.6.2
MAVEN_HOME  C:\apache-maven-3.6.0
ZOOKEEPER_HOME C:\apache-zookeeper-3.5.6-bin

## Update / Verify Path

System Path should include

```Bash
%JAVA_HOME%\bin
%KAFKA_HOME%\bin
%KAFKA_HOME%\bin\windows
%M2_HOME%\bin
%ZOOKEEPER_HOME%\bin
```

## Verify Versions

Open PowerShell here as Administrator and run:

```PowerShell
java -version
mvn -v
```

## Configure Zookeeper

Create the required zoo.cfg. In C:\apache-zookeeper-3.5.6-bin\conf, copy zoo_sample.cfg to zoo.cfg. Open zoo.cfg in Notepad++. Find and edit dataDir=/tmp/zookeeper to dataDir=C:\apache-zookeeper-3.5.6-bin\data

## Configure Kafka

For convenience, copy the C:\kafka_2.12-2.2.0\config\server.properties file from the config folder to the C:\kafka_2.12-2.2.0\bin\windows folder. Open server.properties in Notepad++. Find and edit log.dirs=/tmp/kafka-logs to log.dirs=C:\kafka_2.12-2.2.0\logs

## Start Zookeeper Service

Start the Zookeeper service. Open PowerShell As Administrator (from anywhere) and run the following. Note the port and keep the window open. Zookeeper will run on default port 2181, you can change the default port in <C:\apache-zookeeper-3.5.6-bin\conf\zoo.cfg> file.

```PowerShell
zkserver
```

## Start Kafka Service

Start the Kafka service. Open a new PowerShell As Administrator window in the C:\kafka_2.12-2.2.0\bin\windows folder and run the following. Keep the window open.

```PowerShell
 .\kafka-server-start.bat .\server.properties
```

## Working with Kafka

To run these, open PowerShell as Admininstrator in <C:\kafka_2.12-2.2.0\bin\windows>.

To create a topic called test, run:

```PowerShell
./kafka-topics.bat --zookeeper localhost:2181 --create  --replication-factor 1 --partitions 1 --topic test
```

To delete a topic (e.g. test), run:

```PowerShell
./kafka-topics.bat --zookeeper localhost:2181 --delete --topic test

To list topics, run:

```PowerShell
./kafka-topics.bat --zookeeper localhost:2181 --list
```

To describe a topic (e.g. test), run:

```PowerShell
./kafka-topics.bat --zookeeper localhost:2181 --describe --topic test
```

To write messages to a topic, run:

```PowerShell
./kafka-console-producer.bat --broker-list localhost:9092 --topic test
```

To view the messages on a topic (e.g. test), run:

```PowerShell
./kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test --from-beginning
```

To list the groups, run:

```PowerShell
./kafka-consumer-groups.bat --bootstrap-server localhost:9092 --list
```

## Compile and Build the Fat Jar File

Open PowerShell as Administrator in the root project folder, compile the code using Maven and create an executable jar file. Generated artificacts can be found in the new 'target' folder.

```PowerShell
mvn clean compile assembly:single
```

## Start Consumer

Open PowerShell as Administrator in the root project folder, start the original consumer app using topic test and group1 with:

```PowerShell
java -cp target/kafka-api-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.simple.Consumer test group1
```

## Start Producer

Open a new PowerShell as Administrator in the root project folder, start the Producer app using topic test:

```PowerShell
java -cp target/kafka-api-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.simple.Producer test
```

## Test Communications

1. Type some messages for the Producer.
1. Verify the messages are output by the Consumer.

## See also

<http://cloudurable.com/blog/kafka-tutorial-kafka-producer/index.html>

## Reference

See <https://bitbucket.org/professorcase/h07>.
See <https://bitbucket.org/professorcase/h07>.
