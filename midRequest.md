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
    
    subgraph Response Pipeline
    H[Response] --> G;
    G --> F;
    F --> E;
    E --> D;
    D --> C;
    C --> B;
    B --> A;
    end;
```
