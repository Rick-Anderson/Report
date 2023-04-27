```mermaid
sequenceDiagram
  participant Client
  participant Server
  Client ->> Server: HTTP request
  Server ->> ExceptionHandler: Handle exception
  ExceptionHandler ->> Server: Send response
  Server ->> Client: HTTP response
  Client ->> Server: HTTP request
  Server ->> Hsts: Add HSTS header
  Hsts ->> Server: Send response
  Server ->> Client: HTTP response
  Client ->> Server: HTTP request
  Server ->> HttpsRedirection: Redirect to HTTPS
  HttpsRedirection ->> Server: Send response
  Server ->> Client: HTTP response
  Client ->> Server: HTTP request
  Server ->> StaticFiles: Serve static file
  StaticFiles ->> Server: Send response
  Server ->> Client: HTTP response
  Client ->> Server: HTTP request
  Server ->> Routing: Route request
  Routing ->> Server: Send response
  Server ->> Client: HTTP response
  Client ->> Server: HTTP request
  Server ->> Cors: Allow CORS request
  Cors ->> Server: Send response
  Server ->> Client: HTTP response
  Client ->> Server: HTTP request
  Server ->> Authentication: Authenticate user
  Authentication ->> Server: Send response
  Server ->> Client: HTTP response
  Client ->> Server: HTTP request
  Server ->> Authorization: Authorize user
  Authorization ->> Server: Send response
  Server ->> Client: HTTP response
  Client ->> Server: HTTP request
  Server ->> CustomMiddleware1: Perform custom task
  CustomMiddleware1 ->> Server: Send response
  Server ->> Client: HTTP response
  Client ->> Server: HTTP request
  Server ->> Endpoints: Map request to controller action
  Endpoints ->> Server: Send response
  Server ->> Client: HTTP response
  ```
