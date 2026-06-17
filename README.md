# RNA_Seq_Pipeline_illumina
This pipeline descirbes tools used for RNA_Seq_workflow using Novaseq Se platform

# update software and installation of additional tools
sudo apt update
sudo apt install fastqc bowtie2 stringtie samtools
sudo apt install trimmomatic -y

# check software version
fastqc --version
bowtie2--version
stringtie --version
samtools --version
fastqc --help
java -jar /usr/share/java/trimmomatic.jar -version

# installing R packages 
sudo apt install -y libcurl4-openssl-dev libssl-dev libxml2-dev build-essential # install libraries and compiler tools
sudo apt install -y r-base

# navigate through the desktop
cd /home/miguel/Desktop/Gene_express/DGE/Database

# make directory
mkdir Gene_express
mkdir DGE
mkdir Database

# move into the folder Database
cd Database

# setting up of Anopheles arabiensis genome database for CYP450 genes
https://ftp.ensembl.org/pub/release-110/fasta/anopheles_arabiensis/dna/Anopheles_arabiensis.AaraD1.dna.toplevel.fa.gz

# Unzip Anopheles AgamP4.dna
gunzip Anopheles_arabiensis.AaraD1.dna.toplevel.fa.gz

# view the first few lines of the file
cat Anopheles_arabiensis.AaraD1.dna.toplevel.fa | head

# Index the Anopheles arabiensis for faster alignmnet
bowtie2-build Anopheles_arabiensis.AaraD1.dna.toplevel.fa AaraD1_index

# Setting up the GTF file for Anopheles aranbiensis
##  downloading the GTF files
wget https://ftp.ensembl.org/pub/release-110/gtf/anopheles_arabiensis/Anopheles_arabiensis.AaraD1.110.gtf.gz

## Unzip the GTF file
gunzip Anopheles_arabiensis.AaraD1.110.gtf.gz

## view the first few lines of the GTF files
cat Anopheles_arabiensis.AaraD1.110.fa | head

# Setting up the GFF file
## Make a new file with just the details of the genes from AaraD1
grep -i "CYP\|cytochrome p450\|p450" Anopheles_arabiensis.AaraD1.110.gtf > Anopheles_arabiensis_CYP450.gtf

### to be more specific to P450 genes 
grep -iE "CYP6|CYP9|CYP4|CYP12|cytochrome p450" Anopheles_arabiensis.AaraD1.110.gtf > Anopheles_arabiensis_CYP450.gtf

## view the first few lines of the file
head Anopheles_arabiensis_CYP450.gtf



