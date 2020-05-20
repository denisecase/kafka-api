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

## Configue Kafka

Change server.properties file 

From: 

``log.dirs=/tmp/kafka-logs``

To:

``log.dirs=tmp/kafka-logs``


## Start Zookeeper Service

Start Zookeeper service as you did previously. 

## Start Kafka Service

Start Kafka service. 

## Create the Topic

Create a Kafka topic. 

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
