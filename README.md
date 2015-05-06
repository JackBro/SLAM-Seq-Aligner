SLAM-Seq indexer and aligner
=========
SLAM-Seq aligner is a Burrows–Wheeler transform (BWT) based fast indexer/aligner specialized in allow specific T to C mismatch in some constant ratio and parallelized searching for Next Generation Sequencing data. 

SLAM-Seq aligner is released under GPLv2 with additional restriction so that is only applicable to individuals and non-profits and that any for-profit company must purchase a different license.    

##INSTALL
*Only 64 bits systems are able to compile and run SLAM-Seq aligner.
    
### Run the binary directly without installation 
Please try the precompiled binaries first, most of the linux systems should be able to run SLAM-Seq aligner without any troubles.
```bash
bin/FSU_searcher 		# for linux
bin/FSU_indexer 		# for linux
```

#### Get the latest version of the software
```bash
git clone git@github.com:jhhung/sBWT.git
```

#### Compile the software by typing:
```bash
make
```

##USAGE
#### See help
```
FSU_searcher --help
FSU_indexer --help
```
#### Build genomic index (similar to bowtie-build)
```bash
FSU_indexer --input_file [genome.fa] --output_file [ouput prefix]
```

#### Mapping 
```bash
FSU_searcher --input_file [reads.fq] --index_file [index prefix] --allow_mismatch --thread_number [thread number]
```

##Contact
- Jui-Hung Hung <juihunghung@gmail.com>
- Chia-Hua Chang <CHChang810716@gmail.com>
- Chiung-Po Hsiao <restart0216s@gmail.com>



