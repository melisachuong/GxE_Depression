# Gene Environment Interaction Effects in Depression  

Recent methods exploring GxE effects in depression include genome-wide by environment studies (GWEIS) and PGS by envrionment studies.
Findings from these methods have yielded inconsistent and negligible evidence of GxE effects (Peyrot et al., 2014; Peyrot et al., 2018; Mullins et al., 2016; Coleman et al., 2020; Arnau-Soler et al., 2018; Arnau-Soler et al., 2019).

This is likely due to PGSs and genome-wide variants not capturing much of the genetic variance observed in the highly polygenic and complex trait; depression.

Here we employ a mixed linear method making use of relationship matrices capturing genetic, environmental and genome-by-environment interaction effects. The genomic relationship matrices (GRMs) utilise all available genotyped SNPs and thus, are better measures of genetic variance in comparison to single genome-wide variants and PGSs. We expect this model to yield greater statistical power when exploring GxE effects.  

In this study we are interested in Genome-by-Trauma Exposure interaction effects. We use available genomic and trauma exposure data from the UKB study. 

# Relationship Matrices  

We have a realtively large sample with available genomic and trauma data ~150k, so this would mean we would be creating 150k by 150k matrices. This is not too difficult to compute, however, including these matrices into MLMs (downstream analyses) would be computationally exhaustive.  
So here, I create sub-samples based on geographical location of participants (geographical clusters). I aim to have my cluster samples similar.  

Clusters: 


## Genomic Relationship Matrices (GRMs)  

GRMs represent pair-wise genomic similarity between individuals within the sample. The equation calculating genomic similarity incorporates information on the MAF of alleles and the number of copies each individual has. 

Equation: 

A matrix is formed using GCTA software, where diagonals represent genomic similarity of individuals with themselves (so we expect this to be ~1), and offdiagonals represent pairwise genomic similarities. The offdiagonals can also signify relatedness, e.g. parent/offspring or siblings are likely to exhibit values ~0.5, cousins ~0.125 etc.  

Matrix:

## Environmental Relationship Matrices (ERMs)  

ERMs represent pair-wise trauma exposure similarity between individuals within the sample. Remember, the environmental variable can represent any variable of interest. In this study we are interested in self-reported trauma exposure. 16 questions are available assessing self-reported trauma exposure, these are split into 3 groups capturing childhood, adult and catastrophic trauma.  

To incorporate this information coherently, we utilise the principal components of the available questions: 

Matrices are formed used OSCA software, where diagonals represent trauma exposure similarity of individuals with themselves, and offdiagonals represent pairwise trauma exposure similarities. This is based on the how similar the PC values are between each individual. We use algorithm 1 available within the OSCA software. We create different ERMs for full trauma (using PCs of all 16 trauma questions), childhood trauma (using PCs of only childhood trauma questions), adult trauma (using PCs of only adult trauma questions) and catastrophic trauma (using PCs of only catastrophic trauma questions). 

Matrix:

## Interaction Relationship Matrices (GxE)  

We create matrices representing pairwise genome-by-trauma interaction effect similarity between individuals within the sample. We create the GxE matrices using matrix algebra. Mathematically an interaction effect can be thought of as a multiplication, so we obtain the hadamard product of GRM and available ERMs. To be able to use the hadarmard product, matrices have to have identical components, so here we use participants with COMPLETE data.  

Matrix:

# Mixed Linear Models  

Four different MLMs are conducted with increasing complexity, incorporating the created relationship matrices as random effects within GCTA using a GREML framework.  

Equations:  

# Findings
