Welcome to Whole Genome Sequece (WGS) analysis of head lice

In this tutorial, I will walk you through the steps that I took to analyse a WGS dataset from raw to anaylysis ready. The data is from a non-model organism (refer to about section below) and thus will follow the traditional data-analysis pipelines are are used for human data. The raw sequencing files will be deposited into ncbi in the near future. 

#### About the dataset  

The dataset is from a 'human head lice WGS project' in the Reed Lab at the Florida Museum of Natural History. I used Illumina short paired-end reads that were already demultiplexed to remove barcodes. Dataset was also trimmed based on the quality, which resulted in raw fastq paired-end reads. Process of demultiplexing and trimming is unfortunately not a part of this tutorial. Programs that my colleague used to do this are trimmomatic, fastQC and multiQC.

#### Step 1: Mapping reads to a reference 

This section assumes that you already have a reference genome available for your species. If you don't, there are some additional steps that you need to take to first assemble your raw reads to contigs (not a part of this tutorial).

There are mutiple programs that you can use to align your raw reads to a reference genome. The most commonly used programs are BWA, Bowtie2 and NovoAlign. If you are interested in learning about their performance please refer to this [article](https://pubmed.ncbi.nlm.nih.gov/28286147/) among many that you can find on google scholar. 

##### Command

```markdown
Module load BWA #If you are using a comuputing cluster, you have to load the necessary module before you begin

bwa mem \ #program
-t 32 \ #number of threads to use
-Y \ #tells bwa to use soft clipping on supplimentary reads
-R '@RG\tID:LHA-body.1.1\tLB:NS4444\tPL:ILLUMINA\tPM:NOVASEQ\tSM:"$i"' \ #Read group to identify your samples. GATK requires a RG tag
${FASTAREF} \ #path to your reference genome 
${R1}/${GROUP_CODE}."$i".pair1.truncated.gz \ #raw read pair1
${R1}/${GROUP_CODE}."$i".pair2.truncated.gz \ #raw read pair2
> ${SAMPATH}/${FILE_CODE}_${GROUP_CODE1}_"$i".${PAIR_CODE}.sam;\ #output directory and file name
done 

```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/niyomiw/louse_genome/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
