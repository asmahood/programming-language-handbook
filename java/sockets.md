# Sockets
Sockets are available in the `java.net` package.

## Creating a Socket

### Server Side
To create a new server socket:
```java
int port = 6868;
ServerSocket firstServerSocket = new ServerSocket(port);
```
To establish a connection:
```java
Socket socketConnection = firstServerSocket.accept();
```
To start catching messages, you need to create a new `DataInputStream` object from the `java.io` package:
```java
DataInputStream dataStreamIn = new DataInputStream(socketConnection.getInputStream());
```
To read the data caught by the `DataInputStream`:
```java
String readString = (String)dataStreamIn.readUTF();
```
To close the socket connection:
```java
firstServerSocket.close();
```

### Client Side
To create a new client socket:
```java
String host = "localhost";
int port = 6868;
Socket clientSocket = new Socket(host, port);
```
To send data to the server, create a `DataOutputStream`:
```java
DataOutputStream dataStreamOut = new DataOutputStream(clientSocket.getOutputStream());
```
To write a message:
```java
dataStreamOut.writeUTF("Happy Coding!");
```
The `flush` method on `DataOutputStream` to force the output stream to flush the buffered output so it is written.
```java
dataStreamOut.flush();
```
To close the socket and stream:
```java
dataStreamOut.close();
clientSocket.close();
```
