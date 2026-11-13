flowchart TD
    subgraph Ingress Layer
        A[Caller Calls TFN] -->|SIP Trunking| B[SIP Gateway / SBC]
        B -->|SIP Headers & ANI Lookup| H[Ingress IVR]
    end

    subgraph Core Orchestration & State Layer
        H -->|Incoming Session & SIP Payload| ORCH[Orchestrator / VAIC Engine]
        ORCH -->|Manage Conversation State & Turn Transitions| BOT_STATE[(Bot State Machine)]
    end

    subgraph Integration Middleware Layer
        ORCH -->|Request DTO & Action Trigger| MW[Integration Middleware]
        MW -->|Read / Write Session & Cache| CACHE[(Distributed Cache / Redis)]
        MW -->|DTO Validation & Serialization| DTO_ENG[DTO Contract Engine]
    end

    subgraph Bot & Conversational Tier
        BOT_STATE -->|Active Dialog State| G_Auth[Auth Bot]
        BOT_STATE -->|Active Dialog State| G_Policy[Policy Selection Bot]
        BOT_STATE -->|Active Dialog State| S[Steering Bot]
        
        S -->|Intent & Slot Mapping| E1[Skill Bot: Billing]
        S -->|Intent & Slot Mapping| E2[Skill Bot: Tech Support]
        S -->|Intent & Slot Mapping| E3[Skill Bot: Account Services]
    end

    subgraph Backend API Integration Tier
        G_Auth -->|Action Request DTO| MW
        G_Policy -->|Action Request DTO| MW
        E1 -->|Action Request DTO| MW
        E2 -->|Action Request DTO| MW
        E3 -->|Action Request DTO| MW

        MW -->|Multi-API Fan-out & Orchestration| API_AUTH[(Auth / Identity API)]
        MW -->|Multi-API Fan-out & Orchestration| API_POLICY[(Policy & Entitlement API)]
        MW -->|Multi-API Fan-out & Orchestration| API_BACKEND[(Domain APIs: Billing, CRM, Ticketing)]
    end

    %% CCaaS Escalation
    ORCH -->|Final Session State & DTO Handoff| CCAAS[CCaaS Platform]
