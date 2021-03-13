# Remapping raw fastq files from public single-cell datasets to build a multi-tissue immune cell reference for inflammatory diseases

### Author : Joseph Mears and Fan Zhang
### Date : March 11, 2021


To build a multi-tissue immune cell reference for inflammatory diseases, we obtained raw FASTQ files when available from multiple publicly available single-cell datasets to enable an unbiased comparison and integration. 
We were able to complete the following protocol for realignment and integration of most of the publicly available single-cell datasets below. We believe future studies may benefit from this approach and would like to share our key steps. 

## 1) Download raw fastq files:
- RA synovial cells from dbGaP (Zhang, et al, 2019; phs001457.v1.p1), and dbGaP (Stephenson, et al, 2018; phs001529.v1.p1), SLE kidney cells from dbGaP (Arazi, et al, 2019; phs001457.v1.p1), UC colon cells from Single Cell Portal (Smillie, et al, 2019; SCP259), CD ileum cells from GEO (Martin, et al, 2019; GSE134809), interstitial and pulmonary lung disease from GEO (Reyfman, et al, 2019; GSE122960), and COVID-19 and healthy BALF cells from GEO (Liao, et al, 2020; GSE145926). 

    
## 2) Download latest version of STAR (STAR 2.7.8) in order to use STARsolo. 
- STAR is the alignment program underlying the cellranger software from 10X Genomics, but they recently released a standalone single cell alignment software that can be used independently of cellranger and can mimic closely the results one might get from using cellranger to align. STARsolo is much more friendly to sequencing data generated according to protocols other than 10X such as Dropseq, Cel-seq2, or even C1 Fluidigm. The software can be downloaded according to the instructions found here: https://github.com/alexdobin/STAR

## 3) Generate reference using STARsolo
- Download relevant fa files from ensembl. We downloaded cdna file from : http://ftp.ensembl.org/pub/release-102/fasta/homo_sapiens/cdna/Homo_sapiens.GRCh38.cdna.all.fa.gz, but a newer release-103 is available. 
- Alternatively, one can mimic the aligned output given by cellranger by generating a reference genome from the appropriate cellranger reference. These files can be found at : https://support.10xgenomics.com/single-cell-gene-expression/software/downloads/latest? and the relevant genome for our work can be downloaded from the command line via:
            `wget https://cf.10xgenomics.com/supp/cell-exp/refdata-gex-GRCh38-2020-A.tar.gz` or 
            `curl https://cf.10xgenomics.com/supp/cell-exp/refdata-gex-GRCh38-2020-A.tar.gz`
            
- Run STAR with `--runMode genomeGenerate` in order to generate STAR compatible reference genome
     
- For best agreement with cellranger results, use the following command to generate reference:
         
    `~/STAR-2.7.6a/source/STAR --runThreadN 4 --runMode genomeGenerate --genomeDir mimic-GRCh38-cellranger --genomeFastaFiles /data/srlab/external-data/10xgenomics/refdata-cellranger-GRCh38-3.0.0/fasta/genome.fa --sjdbOverhang /data/srlab/external-data/10xgenomics/refdata-cellranger-GRCh38-3.0.0/genes/genes.gtf --genomeSAsparseD 3`

Or run the following command with your own fasta files:
        
        
    `~/STAR-2.7.6a/source/STAR --runThreadN 4 --runMode genomeGenerate --genomeDir NAME_OF_YOUR_REFERENCE --genomeFastaFiles YOUR_FASTA_FILES --sjdbOverhang YOUR_GTF_FILE`


## 4) Align fastq files and generate count matrices using STARsolo
The alignment command differs depending on the technology used in the experiment. Below are examples of how we aligned fastq files for each of the technologies across the datasets we used.

- Cel-seq2: 
    
        `~/STAR-2.7.6a/source/STAR --genomeDir /path/to/reference/you/created/ --sjdbGTFfile /path/to/gtf_file/you/used/to/generate/reference/NAME.gtf --soloType CB_UMI_Simple --soloCBwhitelist /path/to/technology/relevlant/whitelist.txt --soloCBstart 7 --soloCBlen 6 --soloUMIstart 1 --soloUMIlen 6 --soloBarcodeReadLength 0 --runThreadN 32 --outFileNamePrefix /path/to/output/ --readFilesIn /path/to/R2/file.fastq /path/to/R1/file.fastq`
        
- Drop-seq:
    
        `~/STAR-2.7.6a/source/STAR --genomeDir /path/to/reference/you/created/ --sjdbGTFfile /path/to/gtf_file/you/used/to/generate/reference/NAME.gtf --soloType CB_UMI_Simple --soloCBwhitelist None --soloCBstart 1 --soloCBlen 9 --soloUMIstart 10 --soloUMIlen 8 --soloBarcodeReadLength 0 --outFileNamePrefix --outFileNamePrefix /path/to/output/ --readFilesIn /path/to/R2/file.fastq /path/to/R1/file.fastq`
                
- 10X V1:
        
       `~/STAR-2.7.6a/source/STAR --genomeDir /path/to/reference/you/created/ --sjdbGTFfile /path/to/gtf_file/you/used/to/generate/reference/NAME.gtf --soloType CB_UMI_Simple --soloCBwhitelist /path/to/technology/relevlant/whitelist.txt --soloCBstart 1 --soloCBlen 14 --soloUMIstart 15 --soloUMIlen 10 --soloBarcodeReadLength 0 --outFileNamePrefix --outFileNamePrefix /path/to/output/ --readFilesIn /path/to/R2/file.fastq /path/to/R1/file.fastq`
    
- 10X V2:
    
       ` ~/STAR-2.7.6a/source/STAR --genomeDir /path/to/reference/you/created/ --sjdbGTFfile /path/to/gtf_file/you/used/to/generate/reference/NAME.gtf --soloType CB_UMI_Simple --soloCBwhitelist /path/to/technology/relevlant/whitelist.txt --soloCBstart 1 --soloCBlen 16 --soloUMIstart 17 --soloUMIlen 10 --soloBarcodeReadLength 0 --outFileNamePrefix --outFileNamePrefix /path/to/output/ --readFilesIn /path/to/R2/file.fastq /path/to/R1/file.fastq`
        
Note that whitelists were used if available for the technology. 
More information on running STARsolo and how to mimic cellranger output most closely can be found at: https://github.com/alexdobin/STAR/blob/master/docs/STARsolo.md
    
    
## 5) All done! 
You should have count matrices that you can easily concatenate and analyze together (with proper batch correction!).
        



