# Websocket problem 
this is a temporary project demonstrating a current
myfaces 4.0.0 RC websocket problem

## Requirements
Java 11, Node and maven

## Startup

```bash
mvn clean clean install -DskipTests exec:java -Pstandalone -f pom.xml
```

then target your browser towards

## Usage

http://localhost:8080/wsproblem/wsclient.html

if you now press send msg button you can see in the server console:
OnOpen
Message from the client: hello world

This verifies that a working websocket connection is running

Now to the problem case:

