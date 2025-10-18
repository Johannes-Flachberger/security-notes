**Tags:** #type/method 

---
# CIA triad
confidentiality: keep data private
integrity: keep data un-altered
availabiltiy: keep data accessible

- all 3 elements have to be satisfied, if not everyhting is useless
**on attack side:**
DAD triad: Disclosure, Alternation and Destruction
# Principles of Privileges
The levels of access given to individuals are determined on two primary factors:

-   The individual's role/function within the organisation
-   The sensitivity of the information being stored on the system
## Privileged Identity Management (PIM)
translate a user's role within an organisation into an access role on a system
## Privileged Access Management(PAM)
management of the privileges a system's access role has, amongst other things
# Organizational Security Models
## Bell-La Padula Model
focuses on confidentiality, eg used by military
    
```mermaid
graph TD
    %% Levels from top to bottom
    subgraph TS[Top Secret]
        Bob([Bob])
    end

    subgraph S[Secret]
        Alice([Alice])
    end

    subgraph C[Confidential]
        Dave([Dave])
    end

    %% Allowed actions (Read Down)
    TS -->|Bob can read down| S
    S -->|Alice can read down| C

    %% Forbidden actions (No Read Up)
    S -.->|Alice can't read up| TS
    C -.->|Dave can't read up| S

    %% Layout control
    TS --> S
    S --> C

    %% Styles
    style TS fill:#f4b183,stroke:#333,stroke-width:1px
    style S fill:#f9cb9c,stroke:#333,stroke-width:1px
    style C fill:#ffe599,stroke:#333,stroke-width:1px
```

## Biba Model
focused on keeping integrity

```mermaid
graph TD
    %% Flow direction: Top → Down (High at top, Low at bottom)
    subgraph High[High Integrity]
        Bob([Bob])
    end

    subgraph Medium[Medium Integrity]
        Alice([Alice])
    end

    subgraph Low[Low Integrity]
        Dave([Dave])
    end

    %% Allowed actions
    Medium -->|Read Up| High
    Low -->|Read Up| Medium
    High -->|Write Down| Medium
    Medium -->|Write Down| Low

    %% Forbidden actions
    High -.->|No Read Down| Medium
    Medium -.->|No Read Down| Low
    Medium -.->|No Write Up| High
    Low -.->|No Write Up| Medium

    %% Styles
    style High fill:#b6d7a8,stroke:#333,stroke-width:1px
    style Medium fill:#ffe599,stroke:#333,stroke-width:1px
    style Low fill:#f4b183,stroke:#333,stroke-width:1px
```
