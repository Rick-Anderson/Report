```mermaid
graph TD;
    subgraph Request Pipeline
    A[Exception Handling] --> B[HTTPS Redirection];
    B --> C[Static Files];
    C --> D[Routing];
    D --> E[Authentication];
    E --> F[CORS];
    F --> G[Custom Middleware];
    end;
