# contaminationX
testing new contamination method
There's two scripts. ContaEst is the official one with the new Ll function and 2Methods gives the old results as well.

If you run without args, you get help

angsd -i FINAL_BAM_FILE.bam -r X: -doCounts 1 -iCounts 1 -minMapQ 30 -minQ 20 -out OUTPUT; 

angsd/misc/contamination -b 5000000 -c 154900000 -k 1 -m 0.05 -d 3 -e 20 -h HapMapCEU.gz -a OUTPUT.icnts.gz > OUTPUT_counts; 

Rscript ContaEst.R counts=OUTPUT_counts freqs=HapMapCEU.gz maxsites=1000 nthr=60 outfile=OUTPUT_res;

# Improving readme

# Requirements
angsd http://www.popgen.dk/angsd/index.php/ANGSD

R https://cran.r-project.org

doParallel R package. Can be installed by running the following in R.
```
install.packages("doParallel")
```
Most recent version of ContaEstBoth.R

# Reference data
We distribute the ten reference HapMap panels that we use in <insert publication>.  
  
Coordinates in these files are hg19 and 0-based.
  
A description of how to build these panels is included in the angsd distribution under
```
angsd/RES/getALL.txt
```

# Test data
You can download a test bamfile by running:
```
wget -O test_X.bam https://sid.erda.dk/share_redirect/E7PWk3Kx13
wget -O test_X.bam.bai https://sid.erda.dk/share_redirect/BS0sdufOr6
```
This are X-chromosome reads sequenced in https://doi.org/10.1038/nature14625

# Running with test data

## Create counts
We first want to tabulate the allele counts $n_k$



ñam ñam n_n









