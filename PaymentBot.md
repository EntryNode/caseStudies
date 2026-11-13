````mermaid
flowchart LR
A[Main Bot]
B[CCAAS]
C[Ingress PaymentBot]
D[One time payment flow]
E[Recurring Payment flow]
F{amount!null}
G[collect amount]
H[Send to IVR for credit card collection]
I[Isolated credit card data collection]
J[Collects credit number and cvv]
K{number and cvv Confirmed?}
L[External Credit card verification system]
M[External verification system]
N[tokenGeneration]
O[Save session params before exit]
P{amount confirmed?}
Q{sessionId=New?}
R{onetimePayment?}
S[Collect Token]



subgraph Ingress Layer
        A -->|Intent=Payment| B
        B -->|Transfer to Payment Bot| C
    end
subgraph Payment Bot
        C -->R
        Q-->|No|S
        
        R -->|No|E
        R-->|Yes|D
        D-->Q
        Q-->|Yes|F
        E-->O
        G-->P
        P-->|yes|O
        P-->|No Max 2 retries|G
        O-->H
        
        F -->|No| G
        F -->|Yes| O
    end
subgraph Credit Card collection
        H -->B
        B-->I
        I-->J
        J-->K
        S-->N
        N-->S
        K-->|No Max retries=2| I
        K-->|External Call for confirmation| L
        L-->N
    end
subgraph External system
        L-->M
        M-->L
    end
