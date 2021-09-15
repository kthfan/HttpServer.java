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
## Request:
```java
new HttpServer(){
  public void onRequest(HttpServer.Request request, HttpServer.Response response, Socket socket){
    byte[] byteBody = request.getBody();
    String body = request.getBodyText();
    String version = request.getHttpVersion(); //1.0 1.1 or 2
    String method = request.getMethod(); // GET POST etc.
    String path = request.getPath(); // /page/index.html
    String target = request.getRequestTarget(); // /page/index.html?name=john&age=22
    Map<String, String> params = request.getParameters(); // parsed params eg. name=john&age=22
				
    Map<String, String> headers = request.getHeaders();
    String acceptEncoding = headers.get("Accept-Encoding");
				
    Map<String, String> cookies = request.getCookies(); // parsed from headers
    Map<String, String> sessions = request.getSessions(); // set session id using cookie
  }
}.start():
```
## Response:
```java
new HttpServer(){
  public void onRequest(HttpServer.Request request, HttpServer.Response response, Socket socket){
    //setBody and setBodyByText will overwrite original body
    response.setBody("<h1>original text</h1>".getBytes()); // byte array required
    response.setBodyByText("<h1>overwrite text</h1>");	// String required
				
    response.setHttpVersion("1.1");
    response.setStatusCode(200);
    response.setReasonPhrase("OK");
				
				
    //will overwrite original body
    response.setHeader("Content-Type", "text/html; charset=utf-8");
    //won't overwrite original body
    response.setDuplicateHeader("Access-Control-Allow-Origin", "https://localhost");
				
    response.setCookie("name", "john");
    response.setSession("age", "22");
  }
}.start():
```

