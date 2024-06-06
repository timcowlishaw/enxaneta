
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
    col4 --> syn1
    eth6 --> syn1
    syn1 --> cllb1
    syn1 --> eth7_1
    py5 --> py9_1
    eth3 --> col1
    py9_2 --> cllb2
    cllb4 --> cllb5
    cllb5 --> wrapup
    
    subgraph phase1 [1. La Pinya]
        direction LR

        subgraph py [Computational Thinking 101]
            direction TB
            py1[Bootstrapping with
            the Raspberry Pi] --> py2[Signs and Portents]
            py2 --> py3[Pythonic Norms &
            Community Governance]
            py2 --> py4["..."] --> py5["..."]
            py2 --> py6[Early Querent.py
            Prototyping] --> py7[Querent.py Dev]
            py7 --> py8[More Querent.py Dev]
            py8 --> py7
        end
        
        subgraph eth [Foundations of Ethnography]
            direction TB
            eth1[Ethnography as a Genre] --> eth3[Participant Observation
            & Thick Description]
            eth3 --> eth2
            eth2[Observation Exercises] --> eth3
            eth3 --> eth4[Positionality
            & Reflexivity] --> eth5[Taking Fieldnotes] --> eth6["..."]
            eth4 --> eth2
            eth2 --> eth5
            eth5 --> eth2
        end

        subgraph col [Colla App Research]
            direction TB
            col1[Researching Software
            Ethnographically?] --> col2[Dimensions of the
            Colla App] --> col3["..."] --> col4["..."]
            col1[Researching Software
            Ethnographically?]
        end
    end

    subgraph syn1 [Review & Synthesis?]
        direction TB
    end

    subgraph phase2 [2. Els Folres i Manilles]
        direction TB

        subgraph cllb [Collaborative Exploration?]
            direction TB
            cllb1[Planning?] --> cllb2[Collaborative Coding?]
            cllb1 --> cllb3[Fieldwork?]
            cllb2 --> cllb4[Bogostian Carpentry?]
            cllb3 --> cllb4
        end

        subgraph py9 [More Python?]
            direction TB
            py9_1["..."] --> py9_2["..."]
        end
    end

    subgraph eth7 [Tim's PhD
    Research?]
        direction TB
        eth7_1["..."] --> eth7_2["..."]
    end

    subgraph phase3 [3. El Tronc]
        direction TB

        subgraph cllb5["..."]
            direction TB
            cllb6["..."]
        end
    end