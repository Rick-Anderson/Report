```mermaid
graph LR;
    A((A))-->|v|B((B))
    B-->|v|C((C))
    C-->|v|D((D))
    D--x|Return|C
    C--x|Return|B
    B--x|Return|A

    linkStyle 0 stroke-width:2px,fill:none,stroke:blue;
    linkStyle 1 stroke-width:2px,fill:none,stroke:blue;
    linkStyle 2 stroke-width:2px,fill:none,stroke:blue;
    linkStyle 3 stroke-dasharray: 5 5, stroke-width:2px,fill:none,stroke:red;

```
