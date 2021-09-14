# HttpServer.java
Simple http server implementation using java.

## Basic Usage:
```java
new HttpServer(
  Arrays.asList(80, 8080) // list of port
){
  public void onRequest(HttpServer.Request request, HttpServer.Response response, Socket socket){
    response.setBody("<h1>Hello, world!</h1>");
  }
}.start():
```
