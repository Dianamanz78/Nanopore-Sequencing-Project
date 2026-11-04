# Nanopore-Sequencing-Project

## Research Question
Does predicting whether unknown reads will resolve reduce the time needed to produce long reads compared to normal adaptive sampling method with the additional unknown category method?

## Project Format

The project will implement two pipelines:
- Pipeline #1 will use adaptive sampling(accept/reject decisions) with the addition unknown category using the Readfish package. The Readfish package will repeat unknown reads in the next chunk of data (with the idea that the mapper improves with each new chunk) until the unknown read reaches a decision (accept/reject).
- Pipeline #2 will use the same decision categories along with the Readfish package, but after a read is categorized as unknown, we will predict how many more chunks it will need to resolve (or to get a decision of accept or reject). If an unknown read is predicted to not resolve, then the read will be rejected. If not, then the read will proceed to the next chunk.

Benchmark Evaluation:

## Pipeline #1


