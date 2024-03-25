# PA-Bench: a framework for benchmarking pairwise aligners

## Abstract

### Motivation
The problem of pairwise alignment using Smith-Waterman dynamic programming (DP) has been studied since over 60 years ago,
but there are still many recent advances in the state of the art.
This is for good reason: DP alignment accounts for a significant amount of time in real-world bioinformatics pipelines,
especially with long genomes and recent long read technologies.
In fact, there has been substantial recent work on designing alignment-free algorithms, but DP alignment still provides
gold standard results compared to those methods.

To date, there has not been a scalable and comprehensive benchmark suite for DP aligners.
Many algorithm developers build their own ad-hoc benchmarks, but they fail to account for the diversity of downstream use cases.
For example, it is possible to align reads to genomes, genomes to genomes, reads to other reads, etc.
Pairs of sequences can vary widely, from small substitutions or insertions/deletions (indels), or large structural variations
driven by biology.
This problem is amplified by the rapid increase in sequencing technologies that produce reads with varying error
profiles and length characteristics, including short Illumina reads, long PacBio HiFi reads, ultra-long Oxford Nanopore reads,
and other emerging technologies.
Thus, we set out to build a framework to make it easier for algorithm developers to compare their algorithms with others on a
wide variety of data and allow downstream algorithm users to make informed choices in picking the right algorithms for their
data.

To limit the scope of the benchmarks, we chose to focus on the simplest task of global alignment of DNA sequences.
Although this does not capture the full complexity of real-world use cases, which include semi-global, local, etc. alignment
or other data types like proteins, graphs, etc., this still allows us to better understand the performance characteristics of alignment
algorithms.

### Methods

**Results**: Some plots made using the PaBench.

**Code**: github.com/pairwise-alignment/pa-bench
