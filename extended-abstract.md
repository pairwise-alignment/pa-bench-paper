# PA-Bench: a framework for benchmarking pairwise aligners

Ragnar Groot Koerkamp and Daniel Liu

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
At a high level, PA-Bench consists of wrappers and types for different aligner algorithms for a uniform interface,
a command-line tool for running these wrapper individually,
and a command-line tool for orchestrating a set of jobs for benchmarking different aligners on different datasets.
New aligners can easily be supported by implementing the simple interface.

PA-Bench's main interface takes a YAML file that allows the user to specify datasets (with options to generate sequences or read them from files),
whether to compute tracebacks, alignment cost models, and the alignment algorithms.
Then, it takes the cartesian product of these parameters to get the benchmarking jobs.
These jobs are automatically executed on multiple threads for testing or a single thread for benchmarking.
PA-Bench allows setting limits on the runtime and memory usage of jobs, and it gracefully handles
resource exhaustion or errors.
To test the accuracy of aligners, especially those with heuristic algorithms, PA-Bench verifies the alignment results
by comparing different algorithms.
Additionally, to speed up development iteration time, PA-Bench caches job results by default to avoid rerunning successful jobs.
Finally, PA-Bench outputs benchmark results in `JSON` format, and we provide example scripts to parse and plot
benchmark results.

PA-Bench has proven useful for rapidly testing and benchmarking aligners, and
it has been used in practice to run the benchmarks for A\*PA and discover bugs in other aligners.

### Results
Some plots made using the PA-Bench.

**Code**: github.com/pairwise-alignment/pa-bench
