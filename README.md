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

# setting up of Anopheles gambiae genome database for CYP450 genes
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/150/785/GCA_000150785.1_g4/GCA_000150785.1_g4_genomic.fna.gz

# Unzip Anopheles AgamP4.dna
gunzip GCA_000150785.1_g4_genomic.fna.gz

# view the first few lines of the file
cat GCA_000150785.1_g4_genomic.fna.gz | head 

# Index the Anopheles gambiae for faster alignmnet
bowtie2-build GCA_000150785.1_g4_genomic.fna Agamp4 

# Setting up the GTF file for Anopheles gambiae
##  downloading the GTF files
wget wget http://ftp.ensemblgenomes.org/pub/metazoa/release-63/gtf/anopheles_gambiae/VectorBase-68_AgambiaePEST.gff.gz

## Unzip the GTF file
gunzip VectorBase-68_AgambiaePEST.gff.gz

## view the first few lines of the GTF files
cat VectorBase-68_AgambiaePEST.gff | head

# Setting up the GFF file
## Make a new file with just the details of the genes from AaraD1
grep -i "CYP\|cytochrome p450\|p450" VectorBase-68_AgambiaePEST.gff > Anopheles_arabiensis_CYP450.gtf

### to be more specific to P450 genes 
grep -iE "CYP6|CYP9|CYP4|CYP12|cytochrome p450" Anopheles_arabiensis.AaraD1.110.gtf > Anopheles_arabiensis_CYP450.gtf

## view the first few lines of the file
head Anopheles_arabiensis_CYP450.gtf




