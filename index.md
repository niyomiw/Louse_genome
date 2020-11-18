### Welcome to the Human Head Louse Whole Genome Sequecing Project

In this tutorial, I will walk you through the steps that I took to analyse a WGS dataset from raw to analysis ready. The data is from a non-model organism (refer to about section below) and thus will not follow the traditional data-analysis pipelines that are used for human data. The raw sequencing files will be deposited into ncbi in the near future. 

#### About the dataset  

The dataset is from a 'human head lice WGS project' in the Reed Lab at the Florida Museum of Natural History. I used Illumina short paired-end reads that were already demultiplexed to remove barcodes. Dataset was also trimmed based on the quality, which resulted in raw fastq paired-end reads. Process of demultiplexing and trimming is unfortunately not a part of this tutorial. Programs that my colleague used to do this are trimmomatic, fastQC and multiQC.

#### Step 1: Mapping reads to a reference 

This section assumes that you already have a reference genome available for your species. If you don't, there are some additional steps that you need to take to first assemble your raw reads to contigs (not a part of this tutorial).

There are mutiple programs that you can use to align your raw reads to a reference genome. The most commonly used programs are BWA, Bowtie2 and NovoAlign. If you are interested in learning about their performance please refer to this [article](https://pubmed.ncbi.nlm.nih.gov/28286147/) among many that you can find on google scholar. 

##### Command

```markdown
#If you are using a computing cluster, you have to load the necessary module before you begin
Module load BWA 

bwa mem \ 
-t 10 \ 
-Y \ 
-R '@RG\tID:seq_info.lane\tLB:library_name\tPL:ILLUMINA\tPM:NOVASEQ\tSM:sample_name \ 
path/to/your/reference_genome \ 
path/to/your/raw/reads/sample_name.pair1.truncated.gz \ 
path/to/your/raw/reads/sample_name.pair2.truncated.gz \ 
> path/to/your/output/directory/file_name.sam;\ 
done 

```
What did we specify in the command above? 
We first loaded the module, set the number of threads to 10 (You can change this number depending on how much resources available to you), -Y tells bwa to use soft clipping on supplimentary reads, -R specifies the unique Read groups assigned to your libraries (GATK requires a RG tag to identify each unique sample that comes from multiple libraries). 

