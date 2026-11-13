````mermaid
flowchart TD
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
T[call payment API]
U[Transfer back to Main Bot]
V[External Payment System]
W{Success}

subgraph Ingress Layer
        A -->|Intent=Payment| B
        B -->|Transfer to Payment Bot| C
    end
subgraph Payment Bot
        C-->R
        D-->Q
        E-->O
        F -->|No| G
        F -->|Yes| O
        G-->P
        H-->B
        O-->|Give old Session Details|S
        O-->H
        P-->|yes|O
        P-->|No Max 2 retries|G
        Q-->|No Collect stored Unique ID|O
        Q-->|Yes|F
        R -->|No|E
        R-->|Yes|D
        S-->|call to make payment against Token |T
        V-->T
        U-->B
        
    end
subgraph Credit Card collection
       
        B-->I
        I-->J
        J-->K
        S-->|Request=Token|N
        N-->|Response =Token|S
        K-->|No Max retries=2| I
        K-->|External Call for confirmation| L
        L-->N
    end
subgraph External system
        L-->M
        M-->L
        T-->U
        V-->W
        T-->V
        
    end
