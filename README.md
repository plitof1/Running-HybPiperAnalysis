# Running-Hybpiper

## These are the steps being followed to generate the paralogs
### Environment: 2017 Intel 2.8Ghz Icore 7 based Apple Macbook Pro, 16GB, 256GB storage, MacOS Ventura 13.6.7
### Dependencies
1) final_set_of_exons_formatted.fasta: contains 4,956 genes
2) SRR11028140.fastq: downloaded from NCBI
3) filelist.txt: Just a list of the genes in final_set_of_exons_formatted.fasta
### Steps
1) Run: hybpiper check_targetfile --targetfile_dna final_set_of_exons_formatted.fasta  
        Results: Contains only 1 gene with low_complexity: Assembly-020249.24  
        Output: fix_targetfile_2024-05-23-09_01_07.ctl
3) Run: hybpiper fix_targetfile --targetfile_dna final_set_of_exons_formated.fasta fix_targetfile_2024-05-23-09_01_07.ctl (*.ctl file is output of prior step)  
        Results: Nothing to fix
   Output: fix_targetfile_2024-05-23-09_11_04.log
4) Run: hybpiper assemble -t_dna final_set_of_exons_formatted.fasta -r SRR11028140.fastq --prefix D4-Full --bwa  
        Results:
             Runtime summary info:  
                      [INFO]:    Everything looks good!  
                      [INFO]:    Checking target file FASTA header formatting...  
                      [INFO]:    The target file FASTA header formatting looks good!  
                      [INFO]:    The target file contains at least one sequence for 4956 unique genes.  
                      [WARNING]: There are 3931 sequences in your target file that contain unexpected stop  
                               codons when translated in the first forwards frame. If your target file  
                               contains only protein-coding sequences, please check these sequences, and/or  
                               run "hybpiper fix_targetfile". Sequence names can be found in the sample log  
                               file (if running "hybpiper assemble") or printed below (if running "hybpiper  
                               check_targetfile").  
                   [WARNING]: There are 3277 sequences in your target file that are not multiples of three.  
                               If your target file contains only protein-coding sequences, please check these  
                               sequences, and/or run "hybpiper fix_targetfile". Sequence names can be found in  
                               the sample log file (if running "hybpiper assemble") or printed below (if  
                               running "hybpiper check_targetfile").  
                    [NOTE]:    80 genes had no good matches.  
                    [NOTE]:    Running initial SPAdes assemblies for 4876 genes with reads...
            End of run notes:
                   [INFO]: Generated sequences from 1828 genes!  
                           [WARNING]: 1454 genes contain internal stop codons. See file  
                           "D4-Full_genes_with_non_terminal_stop_codons.txt" for a list of gene names, and  
                           visit the wiki at the following link to view troubleshooting recommendations.  
                           https://github.com/mossmatters/HybPiper/wiki/Troubleshooting,-common-  
                           issues,-and-recommendations#31-sequences-containing-stop-codons  
                   [WARNING]: Potential long paralogs detected for 659 genes!  
                   [WARNING]: Potential paralogs detected via contig depth for 668 genes!  
           Command runtime: 55 minutes  
           Output: D4-Full_hybpiper_assemble_2024-05-23-09_15_14.log
5) Run: hybpiper stats -t_dna final_set_of_exons_formatted.fasta gene filelist.txt  
        Results: It was looking for .bam or .blastx files for each gene, which we don't have  
        Output: hybpiper_stats.tsv - contained just column headers  
                seq_lengths.tsv - results were 0 for all genes     
7) Run: hybpiper retrieve_sequences dna -t_dna final_set_of_exons_formatted.fasta  --samle_names filelist.txt
        Results: No sequences found

   find . -type f -name "*paralogs.fasta"
   
