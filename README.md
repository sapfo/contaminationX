# contaminationX
testing new contamination method
There's two scripts. ContaEst is the official one with the new Ll function and 2Methods gives the old results as well.

If you run without args, you get help

angsd -i FINAL_BAM_FILE.bam -r X: -doCounts 1 -iCounts 1 -minMapQ 30 -minQ 20 -out OUTPUT; 

angsd/misc/contamination -b 5000000 -c 154900000 -k 1 -m 0.05 -d 3 -e 20 -h HapMapCEU.gz -a OUTPUT.icnts.gz > OUTPUT_counts; 

Rscript ContaEst.R counts=OUTPUT_counts freqs=HapMapCEU.gz maxsites=1000 nthr=60 outfile=OUTPUT_res;

# Improving readme

# Requirements
R https://cran.r-project.org
angsd http://www.popgen.dk/angsd/index.php/ANGSD


