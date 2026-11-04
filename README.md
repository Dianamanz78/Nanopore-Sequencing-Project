# Nanopore-Sequencing-Project

Nanopore sequencing is a technique where nucleic acids are processed in real time through a nanopore that is set in an electrically resistant membrane within a flow cell Every time a molecule goes through one of the nanopores, this disrupts the ionic current and produces raw signals which are sent to the basecaller(algorithm that translates the raw signal to the actual DNA/RNA sequence) to produce long reads of the DNA/RNA sequences. 

One of the main concerns that this project aims to focus on for nanopore sequencing is the accuracy of the sequences it produces and the speed per read. Readfish is a package that was developed to make adaptive sampling more practical for large genomes. The idea was that it was designed to make the decision loop work and be configurable, not to make each decision optimal since it uses a hand set rule table. Readfish handles unresolved reads by waiting and retrying with fixed rules. I test whether predicting which unknown reads will resolve lets the pipeline decide earlier, reducing pore time without ejecting more target reads.

## Research Question
Does predicting whether unknown reads will resolve reduce the time needed to produce long reads compared to normal adaptive sampling method with the additional unknown category method?

## Project Format

The project will implement two pipelines:
- Pipeline #1 will use adaptive sampling(accept/reject decisions) with the addition unknown category using the Readfish package. The Readfish package will repeat unknown reads in the next chunk of data (with the idea that the mapper improves with each new chunk) until the unknown read reaches a decision (accept/reject).
- Pipeline #2 will use the same decision categories along with the Readfish package, but after a read is categorized as unknown, we will predict how many more chunks it will need to resolve (or to get a decision of accept or reject). If an unknown read is predicted to not resolve, then the read will be rejected. If not, then the read will proceed to the next chunk.

Benchmark Evaluation:

## Pipeline #1


