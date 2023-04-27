```mermaid
graph TD;
    subgraph Request Pipeline
    A[Exception Handling] -->|request| B[HTTPS Redirection];
    B -->|request| C[Static Files];
    C -->|request| D[Routing];
    D -->|request| E[Authentication];
    E -->|request| F[CORS];
    F -->|request| G[Custom Middleware];
    end;
    
    subgraph Response Pipeline
    G -->|response| F;
    F -->|response| E;
    E -->|response| D;
    D -->|response| C;
    C -->|response| B;
    B -->|response| A;
    end;
