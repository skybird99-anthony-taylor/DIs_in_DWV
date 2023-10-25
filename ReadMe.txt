Publication: Olmo-Uceda, M. J., Muñoz-Sánchez, J. C., Lasso-Giraldo, W., Arnau, V., Díaz-Villanueva, W., & Elena, S. F. (2022). DVGfinder: A Metasearch Tool for Identifying Defective Viral Genomes in RNA-Seq Data. Viruses, 14(5), 1–18. https://doi.org/10.3390/v14051114.

INFORMATION ABOUT DVGFINDER: HOW IT WORKS AND HOW TO ANALYZE THE OUTPUT

-Datasets used in my analysis were the files labeled 'SAMPLE_FILTERED_ML.csv,' as these are the final products of the DVGfinder pipeline

-DVGfinder is more sensitive than either ViReMa or DI-tector seperately. It decays slightly in precision as sample size increases because that happens with DI-tector.

-With small library size (~10^5), DVGfinder Metasearch is the most sensitive and precise. With larger library size (~10^7), DVGfinder Filtered and Consensus is the most sensitive and precise.

DEFINITIONS AND EXPLANATIONS
-BP = RdRp breakpoint (where the RdRp drops off the genome)
-RI = RdRp re-initiation point (where the RdRp re-attaches to the genome)

-RPHT (reads per hundred thousand) = the number of reads where the BP/RI junction has been found relative to the total number of reads that are correctly aligned with the reference sequence. The formula is RPHT=10^5*DVG_read_counts/total_mapped_reads.

-pBP and pRI (proportion of reads in the BP and RI genome coordinates) = the number of reads at coordinate X of an identified DVG with respect to the total mapped reads at that genome coordinate. These values can be >1 because in the first pass of the metasearch algorithm can find pDVGs in reads that do not initially align with the reference genome. The formula is pX=DVG_read_counts/total_depth_in_coordinate_X.

-SDRM = THe semi-difference relative to the mean for the depth value of the BP (a) and the depth value of the RI (b). It can also be thought of as the depth mean in the neighborhood of the BP and RI coordinates. The formula is SDRM=|a-b|/(a+b).

*******The relativized values are what I used for my analysis (e.g., RPHT, pBP, pRI)

CAVEATS
-The machine learning predictor is only applied to case 1 (both ViReMa and DI-tector found the DVG).

-'Length DVG' is just a prediction, assuming that the BP/RI coordinate is the only recombination spot in the DVG. Table 2 in the paper.

-Subgenomic RNAs will be identified by the program as deletion DVGs.

-Lots of repeat sequences can cause failure to exactly place a BP or RI.

-Test datasets were synthetic.

-The program generates a considerable amount of false positives if you are strict with your rule of only counting the EXACT junction as a known DI, but, if you make this rule more lax (30nt pre and post), the FP rate goes way down.