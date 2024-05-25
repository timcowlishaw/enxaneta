
```mermaid
flowchart TB
    prelude(0. Fer Pinya: Preparation)
    phase1(1. La Pinya: Skill Development)
    phase2(2. Els Folres i Manilles: Collaborative Exploration)
    phase3(3. El Tronc: Integration and Application)
    wrapup(4. Desmuntar)
    
    prelude --> py
    prelude --> eth
    phase1 --> phase2
    phase2 --> phase3
    phase3 --> wrapup
    
    subgraph phase1 [1. La Pinya: Skill Development]
        direction LR
        subgraph py [Computational Thinking 101]
            py1[Bootstrapping with the Raspberry Pi] --> py2[Signs and Portents]
            py2 --> py3[etc.]
        end
        
        subgraph eth [Ethnography 101]
            eth1[Core Ethnographic Concepts] --> eth4
            eth3[Observation Exercises]
            eth4 --> eth3
            eth3 --> eth4[Fieldnotes & Thick Description]
        end
    end

    subgraph phase2 [2. Els Folres i Manilles: Collaborative Exploration]
        direction TB
        subgraph cllb [Collaborative Exploration]
            cllb1[Planning] --> cllb2[Collaborative Coding]
            cllb1 --> cllb3[Joint Fieldwork]
            cllb2 --> cllb4
            cllb3 --> cllb4[Bogostian Carpentry]
        end

        subgraph py4 [Intermediate Python?]
            py4_1[???] --> py4_2[???]
        end

        subgraph eth6 [Topics in Ethnographic Research?]
            eth6_1[???] --> eth6_2[???]
        end

    end