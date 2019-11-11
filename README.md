# RNA Sequence Picking After Cutting Enzymatically (aka RNA SPACE)

This repository contains software for the design of DNA oligonucleotides to support the selective enrichment of particular polyadenylated transcripts, viral genomes, etc. using the Oxford Nanopore Technologies (ONT) direct RNA sequencing protocol.  While the existing ONT protocol enriches for polyadenylated RNA, no targeted enrichment method currently exists for a *specific* polyadenylated RNA, such as a particular human gene of interest, or important positive strand RNA virus families (e.g. Coronavirus, Enterovirus, Rhinovirus, Cocksackie)) in human clinical samples. While others have reported succesfully 

The RNA SPACE protocol takes advantage of the unusual property of six DNA restriction enzymes ([AvaII](https://www.neb.com/products/r0153-avaii), [AvrII](https://www.neb.com/products/r0174-avrii), [BanI](https://www.neb.com/products/r0118-bani), [HaeIII](https://www.neb.com/products/r0108-haeiii), [HinfI](https://www.neb.com/products/r0108-haeiii) and [Taq1](https://www.neb.com/products/r0155-hinfi)) to cut the RNA strand in RNA:DNA duplexes to introduce a 3' end that is targetable using the ONT protocol's sequence-specific "RTA Oligo B" probe option.

This software designs two oligonucletide (oligo) probes for any given gene:

  * the "RE" oligo to generate a RNA:DNA duplex in the known transcripts of interest
  * the sequence-specific RTA Oligo B 

## Quick Start

Precalculated oligos for quasi-full length RefSeq transcript elucidation from human or mouse are available at [http://nanopore.space](http://nanopore.space).

## Installation

The software itself is a fairly simple Perl script, with no library dependencies, and so should work out of the box on most Linux systems. BUT...

The designed oligos are checked for undesireable features such as hairpin or dimer formation by using the third party software quikfold from the [mfold package](http://unafold.rna.albany.edu/?q=mfold/download-mfold), which must be downloaded separately. Pre-built mfold suite binaries are available for RedHat/CentOS [here](http://unafold.rna.albany.edu/download/mfold-3.5-Cross-RedHat-binaries.tar.gz), and requires library dependency installation like so:

```bash
yum install libpng12 compat-libf2c-34
```

## Usage

The software expects two files present for any species being designed for: `foo.refMrna.fna` and `foo.mrna_to_gene.txt`. Examples for human (hg19) and mouse (mm10) are included in the repository. Invocation is of the form

```bash
rnaspace <gene name> <species> <design output.txt>
```

For example:

```bash
rnaspace ADH1A hg19 my_outputted_adh1a_design_choices.txt
```
