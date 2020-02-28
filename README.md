# RNA Sequence Picking After Cutting Enzymatically (aka RNA SPACE)

This repository contains software for the design of DNA oligonucleotides to support the selective enrichment of particular polyadenylated transcripts, viral genomes, etc. using the Oxford Nanopore Technologies (ONT) direct RNA sequencing protocol.  While the existing ONT protocol enriches for polyadenylated RNA, no targeted enrichment method currently exists for a *specific* polyadenylated RNA, such as a particular human gene of interest within total mRNA, or important positive strand RNA virus families (e.g. Coronavirus, Enterovirus, Rhinovirus, Cocksackie)) in human clinical samples. The ability to enrich for a small number of transcripts may become increasingly important as nanopore sequencing happens at smaller (less expensive) scale, either through barcode multiplexing or official direct RNA support on the Flongle device.

The RNA SPACE protocol takes advantage of the unusual property of six DNA restriction enzymes ([AvaII](https://www.neb.com/products/r0153-avaii), [AvrII](https://www.neb.com/products/r0174-avrii), [BanI](https://www.neb.com/products/r0118-bani), [HaeIII](https://www.neb.com/products/r0108-haeiii), [HinfI](https://www.neb.com/products/r0108-haeiii) and [Taq1](https://www.neb.com/products/r0155-hinfi)) to cut the RNA strand in RNA:DNA duplexes to introduce a 3' end that is targetable using the ONT protocol's sequence-specific "RTA Oligo B" probe option.

This software designs two oligonucletide (oligo) probes for any given gene:

  * the "RE" oligo to generate a RNA:DNA duplex in the known transcripts of interest
  * the sequence-specific RTA Oligo B 

## Installation

The software itself is a fairly simple Perl script, with no library dependencies, and so should work out of the box on most Linux systems. 

## Usage

The software expects two files present for any species being designed for: `foo.refMrna.fna.gz` and `foo.mrna_to_gene.txt`. Examples for human (hg19) and mouse (mm10) are included in the repository. Uncompressed .fna (FASTA nucleotide) files are also accepted, but git limits individual files to 100MB, so gzip is the default. 

Invocation is of the form

```bash
rnaspace <gene name> <species> <design output.txt>
```

For example:

```bash
rnaspace ADH1A hg19 my_outputted_adh1a_design_choices.txt
```

If you would like to target something other than the further 3' site possible in a transcript, simply place the FastA record in a file, truncated to the part of the transcript you would like, and limit the mrna_to_gene file to the one line describing your FastA file.

The wet lab protocol using the oligos can be found on [protocols.io](https://www.protocols.io/view/enrichment-of-a-specific-polyadenylated-rna-for-na-88ahzse/abstract).

