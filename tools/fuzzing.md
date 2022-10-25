---
title: SBFT'23 Fuzzing Competition Instructions
layout: md
---
# Fuzzing Competition (C/C++ Programs)

## tl;dr

* Register here: [Registration Form](https://forms.gle/QZgUYysoBizeAKRu9) (Deadline: **AoE Friday 6th Jan 2023**)
* Write a fuzzer for C/C++ programs (or choose an existing fuzzer).
* Integrate it into [FuzzBench](https://google.github.io/fuzzbench/getting-started/adding-a-new-fuzzer/)
* Maximize number of bugs found and coverage achieved in 23 hours.
* Get your PR accepted to FuzzBench (Deadline: **24th Feb 2023**).


## Benchmarking Platform
**Fuzzer**. The competing fuzzer must link against a [libFuzzer-style
function](https://llvm.org/docs/LibFuzzer.html#fuzz-target) called
```C
int LLVMFuzzerTestOneInput(const uint8_t *Data, size_t Size);
```
which accepts an array `Data` of size `Size`. The objective of the fuzzer is to generate as many unique crashes as
possible. The fuzzer can leverage any type of feedback from the executed program as guidance towards this objective.

For our competition, we use Google's [FuzzBench](https://google.github.io/fuzzbench) fuzzer evaluation platform
[[ESEC/FSE'21]](https://research.google/pubs/pub50600/). FuzzBench provides an easy API for [integrating
fuzzers](https://google.github.io/fuzzbench/getting-started/adding-a-new-fuzzer/) to contribute to painless, rigorous
fuzzing research evaluations against a set of [benchmark
programs](https://github.com/google/fuzzbench/tree/master/benchmarks) selected from real-world open-source projects
and a set of [state-of-the-art fuzzers](https://github.com/google/fuzzbench/tree/master/fuzzers). FuzzBench allows to
conduct experiments locally and publicly. Once an experiment is concluded, it generates an [evaluation
report](https://www.fuzzbench.com/reports/sample/index.html) with graphs and statistical tests to measure and
visualize the effect size and statistical significance of the comparison across the chosen fuzzers and benchmark
programs.

**Fuzzer Integration**. From the perspective of the fuzzer, FuzzBench provides generic access to:
* The *source code*, the *build process*, and the *executable* of the available benchmark programs.
* The *fuzz harnesses* which translate the fuzz inputs via `LLVMFuzzerTestOneInput` into executions of the programs,
* The *santizers* (i.e., detectors or oracles) that turns a buggy execution into a program crash. Bugs found by custom
participant-specific sanitizers will be ignored.
* The *docker infrastructure* which
* builds an arbitrary program with (your) fuzzer-specific instrumentation,
* runs a specified set of fuzzers on a specified set of programs for a specified time,
* collects coverage and bug finding information.

**Related work**
* [ESEC/FSE'21] "[FuzzBench: An Open Fuzzer Benchmarking Platform and
Service](https://research.google/pubs/pub50600.pdf)",<br /> J. Metzman, L. Szekeres, L.M.R. Simon, R.T. Sprabery, and
A. Arya.
* [ICSE'22] "[On the Reliability of Coverage-Based Fuzzer
Benchmarking](https://mboehme.github.io/paper/ICSE22.pdf)"<br /> M. B&ouml;hme, L. Szekeres, and J. Metzman.
* [CCS'18] "[Evaluating Fuzz Testing](https://dl.acm.org/doi/10.1145/3243734.3243804)"<br /> G. Klees, A. Ruef, B.
Cooper, S. Wei, M. Hicks



## Competition Process
**Registration** (by 6th January).
1. Please prepare a short "tool report" (up to 2 pages in [IEEE conference
format](https://www.ieee.org/conferences/publishing/templates.html); `\documentclass[10pt,conference]{IEEEtran}`
without including the compsoc or compsocconf options) describing the technology and ideas behind the fuzzer you want
to submit to the competition. The tool report is submitted as part of the registration.
2. Please open a pull request (PR) by [forking FuzzBench](https://github.com/google/fuzzbench/fork) and [submitting a
PR](https://github.com/google/fuzzbench/compare). We encourage you to start early and check your code with our CI
tests, but you can edit your PR at any time before the day of the competition (24th Feb.). Feel free to push the
fuzzer implementation itself just right before the deadline.
3. Register here: [Registration Form](https://forms.gle/QZgUYysoBizeAKRu9)


**Preliminaries**. First, we encourage every participant to get familiar with the
[FuzzBench](https://github.com/google/fuzzbench) infrastructure. Create a [private
fork](https://github.com/new/import) of the FuzzBench repository. Install
[prerequisites](https://google.github.io/fuzzbench/getting-started/prerequisites/). You can now run one fuzzer (e.g.,
[`afl`](https://github.com/google/fuzzbench/tree/master/fuzzers/afl)) on one program (e.g.,
[`libpng-1.2.56`](https://github.com/google/fuzzbench/tree/master/benchmarks/libpng-1.2.56)) using [`make
run-afl-libpng-1.2.56`](https://google.github.io/fuzzbench/getting-started/adding-a-new-fuzzer/#testing-it-out). Get
familiar with [fuzzer integration](https://google.github.io/fuzzbench/getting-started/adding-a-new-fuzzer/) to
integrate your own fuzzer into FuzzBench. Get familiar with the [local
setup](https://google.github.io/fuzzbench/running-a-local-experiment) to run multiple fuzzers, including yours, on
multiple programs and get coverage and bug finding reports.

**Preparation**. The participants are encouraged to use the
[programs](https://github.com/google/fuzzbench/tree/master/benchmarks) and infrastructure available at FuzzBench for
their [local evaluation](https://google.github.io/fuzzbench/running-a-local-experiment). The participants can submit
new fuzzers, or add or extend existing fuzzers. The participants are allowed to modify the compilation of the programs
to inject execution feedback for the fuzzer. During development, regularly make sure that [`make
presubmit`](https://google.github.io/fuzzbench/getting-started/contributing-code/#running-unit-tests) succeeds and it
can [build on benchmark
programs](https://google.github.io/fuzzbench/getting-started/adding-a-new-fuzzer/#testing-it-out). It can be quite
pedantic and you don't want to be failed due to trivial errors.

**Competition** (on 24th February 2023).
* The participants publicly integrate their fuzzers into FuzzBench by submitting a [Pull
Request](https://github.com/google/fuzzbench/pulls) and getting it approved for integration. We will only consider
fuzzers that passed all CI tests in the PR and that run for at least 30 minutes.

* The participants submit a short tool report (up to 2 pages in [IEEE conference
format](https://www.ieee.org/conferences/publishing/templates.html); `\documentclass[10pt,conference]{IEEEtran}`
without including the compsoc or compsocconf options) describing the technology and ideas behind the submitted fuzzer
and the experience of integrating into FuzzBench.

**Results**. Finally, the winners will be announced two weeks after the submission.

## Prizes and awards
Will be announced later. Stay tuned!

## Organizers
The fuzzing competition is organized jointly by Abhishek Arya (Google), Oliver Chang (Google), Dongge Liu (Google),
and Marcel Böhme (MPI-SP).

### Google Open Source Security Team (GOSST)
[Abhishek Arya](https://github.com/inferno-chromium), [Oliver Chang](https://github.com/oliverchang), and [Dongge
Liu](https://github.com/Alan32Liu) are with the Google Open Source Security Team (GOSST). The team works to improve
the security of open source software that Google and the world rely on. The team's
[FuzzBench](https://google.github.io/fuzzbench/) provides a free service for researchers to [rigorously evaluate
fuzzers](https://www.fuzzbench.com/reports/sample/index.html) on a wide variety of [real-world
benchmarks](https://github.com/google/fuzzbench/tree/master/benchmarks) at Google's scale. The team's
[ClusterFuzz](https://google.github.io/clusterfuzz/) and [OSS-Fuzz](https://google.github.io/oss-fuzz/) projects
combine modern fuzzing techniques with scalable, distributed execution to make widely used open source software more
secure and stable. GOSST also contributes to hardening the open source supply chain with [SLSA](https://slsa.dev/),
[Sigstore](https://www.sigstore.dev/), and projects in collaboration with the [Open Source Security
Foundation](https://openssf.org/).

### Marcel Böhme (MPI-SP)
Marcel Böhme leads the Software Security research group at the Max Planck Institute for Security and Privacy (MPI-SP)
in Germany. His current research interest is the automatic discovery of security flaws at the very large scale. One
part of his group develops the probabilistic foundations of automatic software testing (i.e., finding bugs by
generating executions) to elucidate fundamental limitations of existing techniques and to explore the assurances that
software testing provides when no bugs are found. The other part of his group develops practical vulnerability
discovery tools that are widely used in software security practice.
