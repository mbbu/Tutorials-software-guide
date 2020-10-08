Connect to https://hpc01.icipe.org/rstudio/auth-sign-in and you can login with your `USERNAME` and the `RSTUDIO_PASSWORD` .

ADA2 should be installed already
```
> library("dada2")
Loading required package: Rcpp
Registered S3 methods overwritten by 'ggplot2':
method from
[.quosures rlang
c.quosures rlang
print.quosures rlang
> packageVersion("dada2")
[1] ‘1.12.1’
```
Looks OK.

## 3. Running the DADA2 Nextflow pipeline on test data

Go to terminal on your R studio GUI
```
$ module load nextflow
```

Do the setup
```
$ cd $HOME
$ git clone https://github.com/h3abionet/16S-rDNA-dada2-pipeline
$ cd $HOME/16S-rDNA-dada2-pipeline
```

Run nextflow
```
$ nextflow run main.nf -profile standard --reads="/data/hbionet/test-data/*_R{1,2}.fastq.gz" --trimFor 24 --trimRev 25 --reference="/data/hbionet/ref-data/silva_nr_v132_train_set.fa.gz" --species="/data/hbionet/ref-data/silva_species_assignment_v132.fa.gz" --outdir="$HOME/out"
N E X T F L O W  ~  version 19.07.0
Launching `main.nf` [exotic_heisenberg] - revision: 1696132777
===================================
uct-cbio/16S-rDNA-dada2-pipeline  ~  version 0.4
===================================
Run Name       : exotic_heisenberg
Reads          : /cbio/data/test-data/*_R{1,2}.fastq.gz
trimFor        : 24
trimRev        : 25
truncFor       : 248
truncRev       : 212
truncQ         : 2
maxEEFor       : 2
maxEERev       : 2
maxN           : 0
maxLen         : Inf
minLen         : 50
rmPhiX         : T
minOverlap     : 20
maxMismatch    : 0
trimOverhang   : F
species        : /cbio/data/ref-data/silva_species_assignment_v132.fa.gz
pool           : pseudo
Reference      : /cbio/data/ref-data/silva_nr_v132_train_set.fa.gz
Max Memory     : 384 GB
Max CPUs       : 40
Max Time       : 3d
Output dir     : /cbio/home/gerrit/out
Working dir    : /cbio/home/gerrit/16S-rDNA-dada2-pipeline/work
Container      : /cbio/containers/16s-rdna-dada2-pipeline.simg
Current home   : /cbio/home/gerrit
Current user   : gerrit
Current path   : /cbio/home/gerrit/16S-rDNA-dada2-pipeline
Script dir     : /cbio/home/gerrit/16S-rDNA-dada2-pipeline
Config Profile : training
=========================================
executor >  local (15)
[fd/c5dfb3] process > runFastQC (rFQC.Dog24)                          [100%] 4 of 4 ✔
[9e/6a2141] process > runMultiQC (rMQC)                               [100%] 1 of 1 ✔
[95/9e5acf] process > filterAndTrim (filterAndTrim)                   [100%] 4 of 4 ✔
[37/15cf0a] process > runFastQC_postfilterandtrim (rFQC_post_FT.Dog2) [100%] 4 of 4 ✔
[-        ] process > runMultiQC_postfilterandtrim                    
[-        ] process > mergeTrimmedTable                               
[dc/19e08d] process > LearnErrorsFor (LearnErrorsFor)                 [100%] 1 of 1 ✔
[7e/62c5a5] process > LearnErrorsRev (LearnErrorsRev)                 [  0%] 0 of 1
[-        ] process > SampleInferDerepAndMerge                        
[-        ] process > mergeDadaRDS                                    
[-        ] process > SequenceTable                                   
[-        ] process > ChimeraTaxonomySpecies                          
[-        ] process > AlignAndGenerateTree                            
[-        ] process > BiomFile                                        
[-        ] process > ReadTracking                                    
```
Looks OK.
