
# Citation
https://academic.oup.com/bioinformatics/article-abstract/36/3/828/5554699

# Requirements
angsd (>=0.922) http://www.popgen.dk/angsd/index.php/ANGSD

R https://cran.r-project.org

doParallel R package. Can be installed by running the following in R.
```
install.packages("doParallel")
```
Most recent version of ContaEstBoth.R

# Reference data
We distribute the ten reference HapMap panels that we use in Moreno-Mayar et al., 2019.  
  
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
These are X-chromosome reads sequenced in https://doi.org/10.1038/nature14625

# Running with test data

## Create counts
We first tabulate the allele counts.
```
angsd -i test_X.bam -r X: -doCounts 1 -iCounts 1 -minMapQ 30 -minQ 20 -out OUTPUT
angsd/misc/contamination -b 5000000 -c 154900000 -k 1 -m 0.05 -d 3 -e 20 -h HapMapFreqs/HapMapCEU.gz -a OUTPUT.icnts.gz > OUTPUT_counts
```
-k 1 Require angsd to output the counts. This is required.

-minMapQ 30 discards reads with mapping quality <30

-minQ 20 discards nucleotides with base quality <20

-b 5000000 -c 154900000 exclude pseudo-autosomal regions

-m 0.05 exclude variants with maf<0.05

-d 3 -e 20 discard sites with a minimum depth of 3 and a maximum of 20

-h HapMapCEU.gz use the HapMap CEU allele frequencies for estimation

An important point: 'HapMapFreqs' folder is present inside our Git repository 'contaminationX'.

## Estimate
```
Rscript bin/ContaEstBoth.R counts=OUTPUT_counts freqs=HapMapFreqs/HapMapCEU.gz maxsites=1000 nthr=4 outfile=OUTPUT_results oneCns=1
```
freqs should be the same file that was used in -h in the previous step. 

counts=OUTPUT_counts use the output from previous step as input

maxsites=1000 resample at most 1,000 blocks for the block jackknife procedure

nthr=4 use four threads (use many of these!)

outfile=OUTPUT_results write results to file called OUTPUT_results

oneCns=1 obtain both One-consensus and Two-consensus estimates

You can get help by running without arguments Rscript ContaEstBoth.R

# Output
Output is a tab-separated file with six columns.
1. Method

2. Contamination point estimate

3. Lower bound for 95% confidence interval

4. Upper bound for 95% confidence interval

5. Error rate (epsilon)

6. Number of overlapping sites between reference panel and sequencing data, after filtering. 

By running the example, you get something like this:

```
One-cns 0.0218110235103631      0.0100863972202939      0.0335356498004323      0.00610110400929692     771
Two-cns 0.022491450054116       0.0102981778438161      0.0346847222644158      0.00610110400929692     771
```




This is a dog :dog:

ñam ñam n_n









