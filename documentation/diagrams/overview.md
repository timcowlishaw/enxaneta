
```mermaid
flowchart TB
    prelude(0. Fer Pinya: Preparation)
    phase1(1. La Pinya: Skill Development)
    phase2(2. Els Folres i Manilles: Collaborative Exploration)
    phase3(3. El Tronc: Integration and Application)
    wrapup(4. Desmuntar)
    
    prelude --> py1
    prelude --> eth1
    phase1 --> cllb1
    py4 --> py5
    eth6 --> eth7
    py5 --> cllb2
    cllb4 --> cllb5
    phase2 --> phase3
    phase3 --> wrapup
    
    subgraph phase1 [1. La Pinya: Skill Development]
        direction LR

        subgraph py [Computational Thinking 101]
            direction TB
            py1[Bootstrapping with the Raspberry Pi] --> py2[Signs and Portents]
            py2 --> py3 --> py4
        end
        
        subgraph eth [Ethnography 101]
            direction TB
            eth1[Core Ethnographic Concepts] --> eth4[Fieldnotes & Thick Description]
            eth1 --> eth3
            eth3[Observation Exercises]
            eth4 --> eth3
            eth3 --> eth4
            eth4 --> eth5 --> eth6
        end
    end

    subgraph phase2 [2. Els Folres i Manilles: Collaborative Exploration]
        direction TB
        subgraph cllb [Collaborative Exploration]
            direction TB
            cllb1[Planning] --> cllb2[Collaborative Coding]
            cllb1 --> cllb3[Joint Fieldwork]
            cllb2 --> cllb4
            cllb3 --> cllb4[Bogostian Carpentry?]
        end

        subgraph py5 [More Python?]
            direction TB
            py5_1 --> py5_2
        end

        subgraph eth7 [Tim's PhD Research?]
            direction TB
            eth7_1 --> eth7_2
        end
    end

    subgraph phase3 [3. El Tronc: Iteration,
    Integration and Application]
        direction TB
        subgraph cllb5 [Iteration?]
    end
end