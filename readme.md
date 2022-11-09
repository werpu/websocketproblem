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

Go to:
http://localhost:8080/wsproblem/wsclient.html

press send message you will get following error in the browser console:

```
    jsfpush.jsf:36 WebSocket connection to 'ws://localhost:8080/wsproblem/jakarta.faces.push/hello?<token>' failed:
```
faces.push.init

The problem is not on the javascript side because the init code is decorated and does a simple ws open
```javascript
         faces.push.init = (socketClientId,
                               url,
                               channel,
                               onopen,
                               onmessage,
                               onerror,
                               onclose,
                               behaviors,
                               autoConnect) => {
             let ws = new WebSocket("ws://localhost:8080"+url);
             ws.onmessage = (message) => console.log(message);
         }
         function onMessage(channel, message,event) {
             alert(message);
         }
```
the code clearly gets a rejection when it tries to open the websocket connection!
The code is pretty similar to the working demo:

```javascript
        var webSocket = new WebSocket("ws://localhost:8080/wsproblem/testws");
        function wsSendMessage() {
            webSocket.send("hello world");
        }
        function wsCloseConnection() {
            webSocket.close();
        }
        function wsOpen(message){
            console.log("Connected:"+message);
        }
        webSocket.onopen = function(message){ wsOpen(message);};
```

Except the working demo bypasses jsf and serves the connection straight over the websocket api!
So the problem lies clearly with our code
