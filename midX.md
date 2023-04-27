```mermaid
graph TD;
    subgraph Request Pipeline
    A[Exception Handling] -->|solid line style| B[HTTPS Redirection];
    B -->|solid line style| C[Static Files];
    C -->|solid line style| D[Routing];
    D -->|solid line style| E[Authentication];
    E -->|solid line style| F[CORS];
    F -->|solid line style| G[Custom Middleware];
    end;
    
    subgraph Response Pipeline
    G -->|dotted line style| F;
    F -->|dotted line style| E;
    E -->|dotted line style| D;
    D -->|dotted line style| C;
    C -->|dotted line style| B;
    B -->|dotted line style| A;
    end;
