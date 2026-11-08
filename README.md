# AFLA CFTR Illumina

Analyses targeted CFTR sequencing from Illumina reads and writes a **one-page report per sample**: small variants with CFTR2 and
ClinVar classes, HGVS and legacy names, poly-T/TG, exon deletions and duplications, and coverage gaps.
Runs in [EPI2ME Desktop](https://epi2me.nanoporetech.com/). **Education and research use only. Not for clinical use.**

## What you need
| Item | Where it comes from |
|---|---|
| EPI2ME Desktop with Docker | [epi2me.nanoporetech.com](https://epi2me.nanoporetech.com/) |
| Paired FASTQ files, one set per sample | Your sequencer, or the AFLA Demux workflow |
| GRCh38 reference FASTA (with `chr` names) | For example the GATK/Broad hg38 analysis set. The workflow can index it. |
| CFTR2 variant list (`.xlsx`) | Download from [cftr2.org](https://cftr2.org) after accepting its usage agreement. Not included here. |
| Ensembl VEP cache, version 115, GRCh38 (optional) | Ensembl; needed for annotation |
| ClinVar GRCh38 VCF with `.tbi` (optional) | NCBI |

## Good to know
- Include **at least 4 samples** from the run. Exon deletions and duplications are found by comparing samples with each other.
- Give your panel's **primer positions** (BED). Without them primer bases count as patient bases, and the report warns you.
- A custom target BED sets where variants are called. Coverage is always judged against the workflow's CFTR target list (all 27 exons
  ±25 bases, poly-T/TG and selected deep intronic sites), so an exon your panel does not cover shows as a gap.
- The report never says a sample is negative outright: it limits the statement to the regions adequately covered.
- Cis/trans cannot be established from short reads. Parental samples are needed.

Install in EPI2ME with **Import workflow** and this repository's address.

## Testing status
Tested end to end on **simulated** data only (known F508del, TG12-5T and a heterozygous exon 2-3 deletion were recovered).
Not yet tested on real Illumina runs, and exon copy-number calling has not been checked on real amplicon depth. Not validated for any
clinical purpose: validate it on your own known samples first.
