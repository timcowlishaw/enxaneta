
```mermaid
flowchart TB
    prelude(0. Fer Pinya)
    phase1(1. La Pinya)
    phase2(2. Els Folres i Manilles)
    phase3(3. El Tronc)
    wrapup(4. Desmuntar)
    
    prelude --> py1
    prelude --> eth1
    prelude --> eth2
    phase1 --> cllb1
    py4 --> py5
    eth5 --> eth6
    py5 --> cllb2
    cllb4 --> cllb5
    cllb5 --> wrapup
    
    subgraph phase1 [1. La Pinya]
        direction LR

        subgraph py [Computational Thinking 101]
            direction TB
            py1[Bootstrapping with the Raspberry Pi] --> py2[Signs and Portents]
            py2 --> py3[...] --> py4[...]
        end
        
        subgraph eth [Ethnography: Foundations & Dimensions]
            direction TB
            eth1[Core Ethnographic Concepts] --> eth3[Fieldnotes & Thick Description]
            eth3 --> eth2
            eth2[Observation Exercises] --> eth3
            eth3 --> eth4[...] --> eth5[...]
        end
    end

    subgraph phase2 [2. Els Folres i Manilles]
        direction TB
        subgraph cllb [Collaborative Exploration?]
            direction TB
            cllb1[Planning?] --> cllb2[Collaborative Coding?]
            cllb1 --> cllb3[Fieldwork?]
            cllb2 --> cllb4
            cllb3 --> cllb4[Bogostian Carpentry?]
        end

        subgraph py5 [More Python?]
            direction TB
            py5_1[...] --> py5_2[...]
        end

        subgraph eth6 [Tim's PhD Research?]
            direction TB
            eth6_1[...] --> eth6_2[...]
        end
    end

    subgraph phase3 [3. El Tronc]
        direction TB
        subgraph cllb5[...]
    end
end