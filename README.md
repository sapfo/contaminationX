# contaminationX
testing new contamination method
There's two scripts. ContaEst is the official one with the new Ll function and 2Methods gives the old results as well.

If you run without args, you get help

/willerslev/users-shared/science-snm-willerslev-bkl835/Scripts/angsd/angsd -i /willerslev/datasets/public/rasmussen_2015_nature/bam/Kennewick_defaultMap1extr.realign.md.head.rmdup.bam -r X: -doCounts 1 -iCounts 1 -minMapQ 30 -minQ 20 -out Test
/willerslev/users-shared/science-snm-willerslev-bkl835/Scripts/angsd/misc/contamination -b 5000000 -c 154900000 -k 1 -m 0.05 -d 3 -e 20 -h /willerslev/users-shared/science-snm-willerslev-bkl835/my_kelvin_data/ContaminationPanels/HapMapCEU.gz -a Test.icnts.gz > Test_counts
Rscript /willerslev/scratch/bkl835/Contamination/3LikTests/ContaEst.R counts=Test_counts freqs=/willerslev/users-shared/science-snm-willerslev-bkl835/jmoreno/ContaminationPanels/HapMapCEU.gz maxsites=1000 nthr=60 outfile=Test_res
-- 
José Víctor Moreno Mayar
Centre for GeoGenetics
University of Copenhagen
