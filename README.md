
<!-- README.md is generated from README.Rmd. Please edit that file -->

This repository contains `R` scripts to extract data and replicate
Conditional Random Fields analyses used in Clark *et al* “Rapid winter
warming could disrupt coastal marine fish community structure” (recently
published in [*Nature Climate
Change*](https://www.nature.com/articles/s41558-020-0838-5))

**Overview**  
We apply [Conditional Random
Fields](http://homepages.inf.ed.ac.uk/csutton/publications/crftut-fnt.pdf)
models to an open-source dataset of fish distributions to show that
winter sea surface warming strongly predicts variation in coastal fish
community compositions in the Mediterranean Sea. Specifically, we
formulate an undirected network model that accounts for all combinations
of other species and environmental covariates (winter and summer sea
surface temperatures) on a species’ occurrence probability. By allowing
species’ co-occurrence associations to vary in response to temperature
changes, our model can generate future biodiversity predictions and
identify putative, biologically-meaningful mechanisms that underlie our
finding of changes in niche filling across seasonal temperature
gradients.

**Authors**  
This work was developed through a collaboration between Nicholas Clark,
James Kerry and Ceridwen Fraser. The `R` code was developed and is
maintained by Nicholas Clark.

**Contacts**  
Please contact [Nicholas
Clark](https://researchers.uq.edu.au/researcher/15140) with any
questions or correspondence.

**Workflow**  
The workflow to extract primary data and complete statistical analyses
is as follows:

1.  Download open-source data on coastal Mediterranean fish species
    occurrences, functional traits and phylogenetic relationships, as
    well as historical and projected [Intergovernmental Panel on Climate
    Change (IPCC) SRES
    A2](https://www.ipcc.ch/site/assets/uploads/2018/03/emissions_scenarios-1.pdf)
    Sea Surface Temperature data, from the open-source
    [FishMed](http://www.esapubs.org/archive/ecol/E096/203/) database
    (Albouy et al. 2015). Note that these data are licensed and cannot
    be directly stored in this repository. However, `R` functions in the
    `Functions` directory are available to download the data directly
    into your working environment. Please follow steps in
    `Workflow/Appendix_S1_Datacollation.pdf` to extract the data.

2.  Run Conditional Random Fields models using functions available in
    the `MRFcov` package (Clark et al. 2018) to analyse the binary
    presence-absence data downloaded in Step 1 above. While `R` code in
    `Workflow/Appendix_S2_Models.pdf` is available to replicate this
    step, note that a previous version of `MRFcov` was used and so some
    of the argument names may have changed but most steps should still
    work. Also please note that these functions were originally run on a
    high-performance computing cluster using 24 processing cores to
    speed up computations. The models will take several hours or more to
    complete even on a powerful machine. We have provided the original
    results to save processing time. These are available in
    `Results/MRF.results.rda` and can be loaded directly into `R` using
    the `load()` command.

3.  Process the models to analyse their results and generate summary
    figures as shown in the original manuscript. The steps are outlined
    in `Workflow/Appendix_S3_ModelProcessing.pdf`. Most of these steps
    should be achievable even on personal laptops, apart from the
    fitting of the multivariate boosted regression trees (which rely on
    the `mvtboost` package, see below for instructions for downloading).
    This step is not partciularly slow but is very memory-heavy because
    each set of `500` regression trees is saved for each of the `215`
    fish species in order to find predictors that minimise joint
    prediction error. We have provided the original results of this step
    to save processing time. These are available in the
    `Results/mvtb.results.rda` and can be loaded directly into `R` using
    the `load()` command.

**Key packages needed for analyses and making
figures**  
`devtools`  
`ggplot2`  
`cowplot`  
`dplyr`  
`plyr`  
`readxl`  
`rvest`  
`tidyverse`  
`stringr`  
`sf`  
`raster`  
`gstat`  
`sp`  
`ape`  
`viridis`  
`MRFcov`  
`mgcv`  
`visreg`  
`PhyloMeasures`  
`pals`(`devtools::install_github('kwstat/pals')`)  
`BBS.occurrences`(`devtools::install_github('nicholasjclark/BBS.occurrences')`)  
`mvtboost`(`devtools::install_github('patr1ckm/mvtboost')`)

**References**  
Albouy, C., Lasram, F.B.R., Velez, L., Guilhaumon, F., Meynard, C.N.,
Boyer, S., Benestan, L., Mouquet, N., Douzery, E., Aznar, R.,
Troussellier, M., Somot, S., Leprieur, F., Le Loc’h, F. & Mouillot, D.
(2015) FishMed: traits, phylogeny, current and projected species
distribution of Mediterranean fishes, and environmental data. *Ecology*,
96, 2312-2313.

Clark, N.J., Wells, K. & Lindberg, O. (2018) MRFcov: Markov Random
Fields with additional covariates. R package version 1.0. GitHub.

Clark, N.J., Kerry, J.T. & Fraser, C.I. (2020) Rapid winter warming
could disrupt coastal marine fish community structure. *Nature Climate
Change* DOI: <https://doi.org/10.1038/s41558-020-0838-5>

*This project is licensed under the terms of the GNU General Public
License (GNU GPLv3)*
