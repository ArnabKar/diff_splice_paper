# Code for differential splicing comparison

This repository contains the code for the following paper comparing various methods for differential isoform usage (differential splicing) detection:

- Soneson, Matthes et al...submitted

One goal of the paper is to contrast different types of differential splicing detection methods (assembly-based, event-based, counting bin-based). Moreover, focussing on the counting-bin based methods, we compare several different ways of defining the counting bins, while keeping the inference engine (DEXSeq) fixed. To evaluate the effect of transcriptome complexity, we perform simulation studies based on both human and fruit fly. 

The structure of this repository is as follows:

- drosophila
	- reference_files/: Directory containing the mean-dispersion estimates used for the simulation
	- run_analysis_drosophila5.sh: Bash script to invoke all analysis steps for the fruit fly simulation. 

- hsapiens
	- reference_files/: Directory containing the mean-dispersion estimates used for the simulation
	- run_analysis_human5.sh: Bash script to invoke all analysis steps for the human simulation. 

- software
	- Rcode: directory containing all R scripts that are called from any of the bash scripts. 

To run the bash scripts, several preparation steps are necessary:

- Install the following software and define the correct path in the beginning of the bash scripts:
	- TopHat2 ([https://ccb.jhu.edu/software/tophat/index.shtml](https://ccb.jhu.edu/software/tophat/index.shtml))
	- Bowtie2 ([http://bowtie-bio.sourceforge.net/bowtie2/index.shtml](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml))
	- samtools (version 0.1.19 necessary for the steps involving rMATS) ([http://www.htslib.org/download/](http://www.htslib.org/download/))
	- SRA toolkit (only needed if the real data fastq files are extracted from an SRA archive) ([http://www.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=software](http://www.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=software))
	- RSEM ([http://deweylab.biostat.wisc.edu/rsem/](http://deweylab.biostat.wisc.edu/rsem/))
	- AStalavista ([http://sammeth.net/confluence/display/ASTA/2+-+Download](http://sammeth.net/confluence/display/ASTA/2+-+Download))
	- cufflinks2 ([http://cole-trapnell-lab.github.io/cufflinks/](http://cole-trapnell-lab.github.io/cufflinks/))
	- MISO ([https://miso.readthedocs.org/en/fastmiso/](https://miso.readthedocs.org/en/fastmiso/))
	- kallisto ([http://pachterlab.github.io/kallisto/](http://pachterlab.github.io/kallisto/))
	- rMATS ([http://rnaseq-mats.sourceforge.net/](http://rnaseq-mats.sourceforge.net/))
	- the script *bedGraphToBigWig* from the UCSC genome browser binary utilities: [http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/](http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/) (For Linux)
	- the script *gtf_to_gff.pl* available here: [https://github.com/mbomhoff/bio-utils/blob/master/gtf_to_gff.pl](https://github.com/mbomhoff/bio-utils/blob/master/gtf_to_gff.pl)

- Download and uncompress reference files and the real data sets used to define the RSEM simulation parameters:
	- The two (paired) fastq files corresponding to the following human sample: [http://www.ebi.ac.uk/ena/data/view/SRR493366](http://www.ebi.ac.uk/ena/data/view/SRR493366)
	- The two (paired) fastq files corresponding to the following fruit fly sample: [http://www.ebi.ac.uk/ena/data/view/SRR1501444](http://www.ebi.ac.uk/ena/data/view/SRR1501444)
	- The human genome fasta file from Ensembl: [ftp://ftp.ensembl.org/pub/release-71/fasta/homo_sapiens/dna/Homo_sapiens.GRCh37.71.dna.primary_assembly.fa.gz](ftp://ftp.ensembl.org/pub/release-71/fasta/homo_sapiens/dna/Homo_sapiens.GRCh37.71.dna.primary_assembly.fa.gz)
	- The human genome gtf file from Ensembl: [ftp://ftp.ensembl.org/pub/release-71/gtf/homo_sapiens/Homo_sapiens.GRCh37.71.gtf.gz](ftp://ftp.ensembl.org/pub/release-71/gtf/homo_sapiens/Homo_sapiens.GRCh37.71.gtf.gz)
	- The fruit fly genome fasta file from Ensembl: [ftp://ftp.ensembl.org/pub/release-70/fasta/drosophila_melanogaster/dna/Drosophila_melanogaster.BDGP5.70.dna.toplevel.fa.gz](ftp://ftp.ensembl.org/pub/release-70/fasta/drosophila_melanogaster/dna/Drosophila_melanogaster.BDGP5.70.dna.toplevel.fa.gz)
	- The fruit fly genome gtf file from Ensembl: [ftp://ftp.ensembl.org/pub/release-70/gtf/drosophila_melanogaster/Drosophila_melanogaster.BDGP5.70.gtf.gz](ftp://ftp.ensembl.org/pub/release-70/gtf/drosophila_melanogaster/Drosophila_melanogaster.BDGP5.70.gtf.gz)