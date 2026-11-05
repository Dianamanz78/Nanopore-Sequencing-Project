# Nanopore-Sequencing-Project

Nanopore sequencing is a technique where nucleic acids are processed in real time through a nanopore that is set in an electrically resistant membrane within a flow cell Every time a molecule goes through one of the nanopores, this disrupts the ionic current and produces raw signals which are sent to the basecaller(algorithm that translates the raw signal to the actual DNA/RNA sequence) to produce long reads of the DNA/RNA sequences. 

One of the main concerns that this project aims to focus on for nanopore sequencing is the accuracy of the sequences it produces and the speed per read. Readfish is a package that was developed to make adaptive sampling more practical for large genomes where it was designed to make the decision loop work and be configurable. However, it was not made to be decision optimal since it uses a hand set rule table. Every time a read is put in the unknown category, the read will wait until it is run in the next chunk and be retried again with fixed rules. This project will see whether predicting how those reads will resolve might potential let the pipeline decide earlier and reduce time. 

## Research Question
Does predicting whether unknown reads will resolve reduce the time needed to produce long reads compared to normal adaptive sampling method with the additional unknown category method?

## Project Format

The project will implement two pipelines:
- Pipeline #1 will use adaptive sampling(accept/reject decisions) with the addition unknown category using the Readfish package. The Readfish package will repeat unknown reads in the next chunk of data (with the idea that the mapper improves with each new chunk) until the unknown read reaches a decision (accept/reject).
- Pipeline #2 will use the same decision categories along with the Readfish package, but after a read is categorized as unknown, we will predict how many more chunks it will need to resolve (or to get a decision of accept or reject). If an unknown read is predicted to not resolve, then the read will be rejected. If not, then the read will proceed to the next chunk.

Benchmark Evaluation:

## Pipeline #1

This pipeline uses the following tools: Squigulator, Minimap2, Icarust, Dorado, and Readfish. Below is the framework of the pipeline:

```mermaid
flowchart TD
    subgraph S1["Stage 1: Offline"]
        A[Squigulator<br/>simulated signal] --> B[Dorado<br/>basecalling]
        A --> T[truth.paf<br/>answer key]
        B --> C[Replay script<br/>chunk and map with minimap2]
        C --> D{Rule table}
        D -->|accept| E[Keep]
        D -->|reject| F[Eject]
        D -->|unknown| G[Retry next chunk]
        G --> C
    end
    subgraph S2["Stage 2: Live"]
        H[Icarust<br/>simulated sequencer] --> I[readfish]
        I --> J[Dorado + minimap2]
        J --> K{Rule table}
    end
    E --> Z[Score against truth.paf]
    F --> Z
    T --> Z
```

