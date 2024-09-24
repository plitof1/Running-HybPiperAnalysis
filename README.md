The HybPiperAnalysis perl script consolidates all of the steps into a single application. The script will run each of the following step to collect the necessary data, if needed, and run each of the HybPiper tasks:

1) Create a standardized subdirectory structure for the DNA species analysis
2) Download, if necessary, a DNA FASTQ Read file
3) If necessary, "trim" the FASTQ file using Trimomatic
4) UnZip the output from the Trimomatic processing
5) Create a "NameList", which will be used in subsequent steps, based on the FASTQ read file name(s)
6) Run HybPiper Assemble
7) Run HybPiper Stats
8) Run HybPiper Retrieve_Sequences
9) Run HybPiper Paralog_Retriever
10) Cleanup/delete HybPiper results files that do not contain any data


### Command line options
Format: perl {app path}/hybpiper.pl --targetfile {filename} --readfile {filename} --analysisdir {path} --datadir {path} --dnaoraa {dna/aa} --cpus {#} --execute {yes/no} --confirm {yes/no}  

Required options  
  - targetfile : the name of the .fasta file to be analyzed   
  - readfile   : the name of the .fastq file to compare to the targetfile    
        -        this will be downloaded from the NCBI (Nation Library of Medicine's National Center for 

Biotechnology Information)  
  --analysisdir: the path to the species directory you want the analysis to be performed in  
                 For example: Czech-Hybseq/Dracula_lotax.  It will be appended to your 'Home Directory'.  
                 The 'Home Directory' is set in the app and depends on OS.  
                 It will be something like /{directory}/{subdir}/Botany/Analysis  
                 Therefore the fully qualified species dir will be: /{directory}/{subdir}/Botany/Analysis/Czech-Hybseq/Dracula_lotax   

Optional options  
  --datadir: Default {analysisdir}/data  
             this is where the data being used for each speices analysis will exist.  
             the 'targetfile', the 'readfile(s)' and the 'namelist.txt'  
             the readfile, as mentioned above will be downloaded from the NCBI repostiory  
             the 'namelist.txt' file will be generated in the HybPiperAnalysis script  
  --dnaoraa: 'dna' or 'aa' (amino acids). Default is 'dna'. Is based on the kind of analysis you want to perform.  
  --cpus   : Default is 1 less than the computers total.  This could be 'processors', 'cores' or 'hyperthreads' depending on the computer  
             This is the number of cpus you want to give to HybPiperAnalysis assemble to use for the assemble process.  
  --execute: 'yes' or 'no'. Default is 'yes'. If 'no' will display the steps it will take but will not execute the functions  
  --confirm: 'yes' or 'no'. Default is 'yes'.  Will pause processing after the Command Line Arguments screen is displayed.  
             Let's the User decide if they want to proceed or not.  If you are going to create a bash script to run HybPiperAnalysis  
             for a number of different readfiles it will be a good idea to set this value to 'no'.  
</pre>

Example: perl ../apps/hybpiperanalysis.pl --targetfile orchidaceae963.fasta --readfile SRR11028166 --analysisdir Czech-Hybseq/Dracula_lotax  

