```mermaid
graph TD;
    subgraph Request Pipeline
    A[Exception Handling] -->|solid| B[HTTPS Redirection];
    B -->|solid| C[Static Files];
    C -->|solid| D[Routing];
    D -->|solid| E[Authentication];
    E -->|solid| F[CORS];
    F -->|solid| G[Custom Middleware];
    end;
    
    subgraph Response Pipeline
    G -->|dotted| F;
    F -->|dotted| E;
    E -->|dotted| D;
    D -->|dotted| C;
    C -->|dotted| B;
    B -->|dotted| A;
    end;
