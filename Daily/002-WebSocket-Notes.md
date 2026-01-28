# Spring Boot WebSocket Today Learning :

## WebSocket Annotations :
### `@EnableWebSocketMessageBroker`
* Stmop message broker enable 
* Spring is divided into websockets that are sending us messages

### `@Configuration`
* This is a configuration class.
* contains settings related to WebSockets.

### `@MessageMapping`
* Maps incoming messages from the client to a controller method.
* Works like @PostMapping in REST but for WebSocket.

### `@SendTo`
* Specifies the destination where the return message should be sent.
* All subscribed clients receive the message.

### `@Payload`
* Binds the message body to a method parameter.
* Converts incoming JSON data into a Java object.


## What is Stomp :
* STOMP (Simple Text Oriented Messaging Protocol) is a messaging protocol used over WebSocket.
It defines rules for sending, subscribing, and routing messages between client and server.

## What is /topic/public :
* `/topic/public` is a broadcast destination in Spring WebSocket.
* All clients who subscribe to this topic receive the message sent to it.

## What is `/app` :
* `/app` is the prefix used for messages sent from client to server.
* It maps to methods annotated with `@MessageMapping`.