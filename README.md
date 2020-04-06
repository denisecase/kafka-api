# kafka-api

Example Kafka Producer and Consumer apps.

Article: <https://www.javaworld.com/article/3060078/big-data/big-data-messaging-with-kafka-part-1.html>

Source: https://github.com/denisecase/kafka-api

## Recommended Environment

* [VS Code](https://code.visualstudio.com/)
* [VS Code Extension - Java Extension Pack](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)

## Prerequisities

* OpenJDK or JDK (8 or up)
* Apache Zookeeper, installed and working
* Apache Kafka, installed and working

You may want to upgrade. For example, using Chocolatey:

Open PowerShell as Administrator (anywhere) and run

```PowerShell
choco upgrade vscode -y
choco upgrade openjdk -y
refreshenv
```

Or:

```PowerShell
choco upgrade all -y
refreshenv
```

## Install Zookeeper (Separate from Kafka)

Install Zookeeper separate from Kafka. Follow the instructions provided or use Chocolatey:

Open PowerShell as Administrator (anywhere) and run:

```PowerShell
choco install apache-zookeeper -y
refreshenv
```

## Install Maven

Install Maven. Follow the instructions provided or use Chocolatey:

Open PowerShell as Administrator (anywhere) and run:

```PowerShell
choco install maven -y
refreshenv
```

## Verify Installations

Open PowerShell here as Administrator and run:

```PowerShell
java -version
mvn -v
```

### Set/Verify Zookeeper System Environment Variable

Windows + Edit System Environment Variables / Environment Variables / System Variables:

Variable name: ZOOKEEPER_HOME
Variable value: C:\apache-zookeeper-3.5.6-bin

### Set/Verify Other Environment Variables

Verify other system environment variables. 

Important! Verify each path exists using the Windows File Explorer.

Your paths may be different - these are the ones on my machine:

```Bash
JAVA_HOME   C:\Program Files\OpenJDK\jdk-14
KAFKA_HOME  C:\kafka_2.12-2.4.1
M2_HOME     C:\ProgramData\chocolatey\lib\maven\apache-maven-3.6.3
ZOOKEEPER_HOME C:\apache-zookeeper-3.5.6-bin
```

### Set/Verify Path

System Path should include the following (using the variable or the full path works - you don't need both)

Using variables:

```Bash
%JAVA_HOME%\bin
%KAFKA_HOME%\bin
%KAFKA_HOME%\bin\windows
%M2_HOME%\bin
%ZOOKEEPER_HOME%\bin
```

Using Full Path (instead of variables):

```Bash
C:\Program Files\OpenJDK\jdk-14\bin
C:\kafka_2.12-2.4.1\bin
C:\kafka_2.12-2.4.1\bin\windows
C:\ProgramData\chocolatey\lib\maven\apache-maven-3.6.3\bin
C:\apache-zookeeper-3.5.6-bin\bin
```

Important!  Multiple Java entries in your PATH will cause problems.  
For example, now that I use OpenJDK, I deleted old Oracle Java entries from my path like these:

```Bash
C:\Program Files (x86)\Common Files\Oracle\Java\javapath
C:\ProgramData\Oracle\Java\javapath
C:\Program Files\Java\jdk1.8.0_162\bin
C:\Program Files\Java\jdk1.8.0_231\bin
```

## Configure Zookeeper

Configure the independent Zookeeper. 

1. In C:\apache-zookeeper-3.5.6-bin\conf, copy zoo_sample.cfg to zoo.cfg.
2. Edit zoo.cfg:

Change:

```Bash
dataDir=/tmp/zookeeper
```

to:

```Bash
dataDir=C:\apache-zookeeper-3.5.6-bin\data
```

## Configure Kafka

Simplify later commands by moving the Kafka configuration file to the same folder as the executables.

1. Copy C:\kafka_2.12-2.4.1\config\server.properties to C:\kafka_2.12-2.4.1\bin\windows.
2. If needed, edit server.properties (in C:\kafka_2.12-2.4.1\bin\windows):

Change:

```Bash
log.dirs=/tmp/kafka-logs
```

to:

```Bash
log.dirs=tmp/kafka-logs
```

## Start Zookeeper Service

Start Zookeeper service. 
Open PowerShell As Administrator (from anywhere) and run the following. 

Note the port and keep the window open. 
Zookeeper will run on default port 2181, you can change the default port in the zoo.cfg file.

```PowerShell
zkServer
```

## Start Kafka Service

Start Kafka service. 
Open a new PowerShell As Administrator window in the C:\kafka_2.12-2.4.1\bin\windows folder and run the following. 

Keep the window open.

```PowerShell
 .\kafka-server-start.bat .\server.properties
```

## Working with Kafka - Understand These Commands

To run these, open PowerShell as Admininstrator in <C:\kafka_2.12-2.4.1\bin\windows>.

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
java -cp target/kafka-api-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.simple.ProducerHello test
java -cp target/kafka-api-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.simple.ProducerSentence test
java -cp target/kafka-api-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.simple.ProducerSentenceRandom test
```

## Test Communications

1. Type some messages for the Producer.
1. Verify the messages are output by the Consumer.

## See also

<http://cloudurable.com/blog/kafka-tutorial-kafka-producer/index.html>

## More about "Edit System Environment Variables"

Setting your system environment variables is important when running Windows and using Linux-based tools. 

To edit:

1. Hit the Windows key and type "Edit the System Environment Variables" until it appears.

1. Click on the menu option to open it.

1. Click "Environment Variables" button.

1. There are two areas.  Don't use the top "user variables" - use the "Systemv variables" below.

1. They are alphabetical - scroll to verify each entry uses the path on your machine.

Here's how to edit the Path variable.

[Image](../blob/masterREADME-figSystemEV.png?raw=true)

Here's the entries you should see.

[Image](../blob/master/README-figSystemPATH.png?raw=true)
